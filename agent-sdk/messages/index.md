---
title: Sending messages | Letta Docs
description: Stream turns and process reasoning, assistant messages, tool calls, and results
---

Send a message with `session.send()` and read the response with `session.stream()`. The stream yields typed events for the whole turn — reasoning, assistant text, tool calls, tool results — and terminates after the turn’s `result` message, so each turn is one `send()` plus one `for await` loop.

Text streams incrementally: `assistant` and `reasoning` arrive as several messages, each carrying the next fragment of `content`. Write fragments as they arrive, or read the turn’s complete assistant text from `result.result` at the end. If you need to reassemble fragments into rows — for a transcript UI, or to store them — read [Message identity](#message-identity) first; using the wrong identifier is the most common source of duplicated messages.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


await using session = client.resumeSession(agentId);


await session.send(
  "Run exactly `echo hello-from-docs` in the shell, then tell me what it printed.",
);


const announcedTools = new Set<string>();
for await (const message of session.stream()) {
  switch (message.type) {
    case "reasoning":
      // Fragments arrive in order and concatenate to the full text:
      // { type: "reasoning", content: " The user wants me to run a", uuid: "message-…c14df", otid: "…", seqId: 3, runId: "run-…" }
      // { type: "reasoning", content: " simple echo", uuid: "message-…c14df", otid: "…", seqId: 4, runId: "run-…" }
      process.stdout.write(message.content);
      break;
    case "tool_call":
      // Tool arguments stream too — each fragment carries the next chunk of
      // rawArguments; toolInput is not parseable until the fragments complete:
      // { type: "tool_call", toolCallId: "chatcmpl-tool-3de0…", toolName: "Bash", rawArguments: '"command": "echo hello', … }
      if (!announcedTools.has(message.toolCallId)) {
        announcedTools.add(message.toolCallId);
        console.log("\ntool:", message.toolName);
        // → tool: Bash
      }
      break;
    case "tool_result":
      // Complete in a single message:
      // { type: "tool_result", toolCallId: "chatcmpl-tool-3de0…", content: "hello-from-docs", isError: false, … }
      console.log("tool result:", message.content);
      break;
    case "assistant":
      // { type: "assistant", content: "The command printed:", uuid: "message-…71e5e1", otid: "…", seqId: 2, … }
      // { type: "assistant", content: " `hello-from-docs`.", uuid: "message-…71e5e1", otid: "…", seqId: 3, … }
      process.stdout.write(message.content);
      break;
    case "result":
      // {
      //   type: "result", success: true,
      //   result: "The command printed: `hello-from-docs`.",
      //   stopReason: "end_turn", durationMs: 3371,
      //   conversationId: "conv-3f5b5985-…",
      //   runIds: ["run-fd5ec0b8-…", "run-52251ce8-…"]
      // }
      if (!message.success)
        console.error(message.errorCode, message.errorDetail);
      break;
  }
}
```

## Message types

`stream()` yields the `SDKMessage` union. The ones most applications handle:

| Type          | Key fields                                       | Meaning                                                                  |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------ |
| `init`        | `agentId`, `conversationId`, `model`, `dreaming` | Session initialization details                                           |
| `reasoning`   | `content`                                        | The agent’s thinking, streamed as ordered fragments                      |
| `assistant`   | `content`                                        | Assistant text for the user, streamed as ordered fragments               |
| `tool_call`   | `toolName`, `rawArguments`, `toolCallId`         | The agent invoked a tool; arguments stream across fragments              |
| `tool_result` | `content`, `isError`, `toolCallId`               | Output of a tool call, complete in one message                           |
| `result`      | `success`, `result`, `errorCode`, `durationMs`   | The turn finished (with the full final text); the stream ends after this |

The union also includes `error` (a failure with full detail), `retry` (an automatic retry is in progress), `queue_update` (messages queued behind the active turn), `stream_event` (token-level deltas), and `loop_status`.

### Handle errors

When a turn fails, the stream emits an `error` message followed by a failed `result`. The `error` message carries the real detail; on the `result`, prefer `errorCode` over the legacy `error` string:

```
for await (const message of session.stream()) {
  if (message.type === "error") {
    console.error(message.message, message.errorDetail);
  }
  if (message.type === "result" && !message.success) {
    console.error("turn failed:", message.errorCode);
  }
}
```

`errorCode` values include `"llm_api_error"`, `"max_steps"`, `"interrupted"`, `"stream_closed"`, `"protocol_error"`, and approval-conflict codes. If the connection closes mid-turn, the closed session cannot be reused — call `resumeSession(conversationId)` to continue in a new session.

### Token-level streaming

For live typing indicators, handle `stream_event` messages with the `extractStreamTextDelta` helper, which normalizes assistant and reasoning deltas:

```
import { extractStreamTextDelta } from "@letta-ai/letta-agent-sdk";


for await (const message of session.stream()) {
  if (message.type === "stream_event") {
    const delta = extractStreamTextDelta(message.event);
    // → { kind: "assistant", text: "The command printed:" }
    // → null for non-text events (usage statistics, tool lifecycle, …)
    if (delta) process.stdout.write(delta.text);
  }
}
```

## Message identity

Streamed messages carry several identifiers. Each answers a different question, and using one to answer another’s question is the most common cause of duplicated, merged, or lost rows in client applications:

| Field        | Answers                                    | Use it for                                                            | Do not use it for                      |
| ------------ | ------------------------------------------ | --------------------------------------------------------------------- | -------------------------------------- |
| `seqId`      | ”Have I already processed this position?”  | Replay suppression after a resume or reconnect; ordering within a run | Row identity                           |
| `otid`       | ”Which message slice does this belong to?” | Reassembling streamed fragments into rows                             | A universal key for every message type |
| `uuid`       | ”Which message object is this?”            | Message identity; cursoring and history backfill                      | Replay suppression                     |
| `toolCallId` | ”Which tool call is this about?”           | Merging tool-call arguments with their tool result                    | Assistant or reasoning identity        |

Rules that follow:

- **Accumulate `assistant` and `reasoning` fragments keyed by message type together with `otid`**, not by `uuid` and not by `otid` alone. Two slices of different kinds can share one `uuid` and differ only by `otid` and type:

  ```
  // Same uuid, different message kinds — keying on uuid merges thinking into the reply
  { type: "assistant",  content: "answer",  uuid: "message-shared", otid: "message-shared-0", seqId: 41 }
  { type: "reasoning",  content: "thought", uuid: "message-shared", otid: "message-shared-1", seqId: 42 }
  ```

  Conversely, a provider can reuse an `otid` across kinds, so key on the pair. When `otid` is absent, fall back to `uuid` *within that message family* — do not apply one generic fallback chain to every type.

- **Never use `seqId` as a row key.** It is a per-run cursor: compare it only within the same `runId`, and reset your threshold when a new run starts.

- **`uuid` is not always a server ID.** It is the top-level message ID when the stream provides one, and an SDK-generated identifier otherwise.

- **Merge tool arguments and results by `toolCallId`**, which is stable across the `tool_call` fragments and the matching `tool_result`. Do not flatten every tool-family message to it — the message envelope and the tool payload are different things. Only `assistant` and `reasoning` messages carry `otid` and `seqId`; tool messages carry `toolCallId` and `uuid`, which is why one generic fallback chain cannot work.

- **If you fetch history mid-turn** (for example, `listMessages()` after a reconnect while a turn is still streaming), rebase your in-progress accumulators onto the fetched rows. Otherwise later fragments keep appending to a stale baseline and the row appears twice.

### Let the SDK do it

Rather than implementing these rules yourself, use the accumulator the SDK exports. It applies typed-by-family merging, per-run replay suppression, and `toolCallId` payload merging for you, and gives you rows to render:

```
import { createTranscriptAccumulator } from "@letta-ai/letta-agent-sdk";


const transcript = createTranscriptAccumulator();


await session.send("Summarize yesterday's deploys.");


for await (const message of session.stream()) {
  const rows = transcript.apply(message);
  render(rows);
}
```

When you merge history — after a reconnect, or when loading older messages — rebase the accumulator onto the fetched page instead of letting in-progress fragments append to a stale baseline:

```
const history = await session.listMessages({ order: "desc", limit: 50 });
transcript.rebase(history);
```

The accumulator is available from both the package root and the portable `@letta-ai/letta-agent-sdk/client` entry, so browser applications get the same behavior.

### Correlate optimistic input

To match a row you rendered optimistically with the row that comes back, pass your own `otid` when sending:

```
const otid = crypto.randomUUID();
renderOptimisticUserMessage({ otid, text });


await session.send(text, { otid });
```

The same `otid` appears on the persisted message, so your client can reconcile the optimistic row instead of discarding local state and re-projecting the whole transcript.

## Message content

`send()` accepts a string or an array of content items, including images:

```
import { imageFromFile } from "@letta-ai/letta-agent-sdk";


await session.send([
  { type: "text", text: "What's wrong with this dashboard?" },
  imageFromFile("./dashboard.png"),
]);
```

In Node.js, import `imageFromBase64` and `imageFromURL` from `@letta-ai/letta-agent-sdk`. In browser and React Native applications, create an `ImageContent` value directly. See [Browser and React Native](/agent-sdk/browser#send-messages-from-a-browser-or-react-native-application/index.md).

## Queueing

Cloud, remote, and local sessions accept another `send()` while a turn is streaming. The runtime owns queueing, and `stream()` may emit `queue_update` events before the current turn’s `result`:

```
for await (const message of session.stream()) {
  if (message.type === "queue_update") {
    // → { type: "queue_update", queue: [] }
    // → { type: "queue_update", queue: [{ id: "…", kind: "user_message", enqueuedAt: "…", … }] }
    console.log("queued turns:", message.queue.length);
  }
}
```

Remove queued work with `session.removeQueuedMessage(itemId)`.

## Handle permission requests

Tool calls that need approval flow through the session’s `canUseTool` callback, governed by the session’s permission mode. See [Permissions](/agent-sdk/permissions/index.md) for modes, interactive approvals, editing tool inputs, and recovering approvals that were pending when a connection dropped.

## Interrupt a turn

Call `abort()` to stop the active turn without closing the session:

```
await session.send("Run the full test suite and fix failures.");


setTimeout(() => {
  void session.abort();
}, 5_000);


for await (const message of session.stream()) {
  if (message.type === "result") break;
}
```

## Change model and reasoning effort

Inspect the model catalog and update the model between turns:

```
const catalog = await session.listModels();
// catalog.entries[0] → {
//   id: "auto", handle: "letta/auto", label: "Auto",
//   description: "Automatically select the best model",
//   isDefault: true, isFeatured: true, free: true,
//   updateArgs: { parallel_tool_calls: true, context_window: 140000, … }
// }
const target = catalog.entries.find(
  (entry) => entry.handle === "anthropic/claude-opus-4-8",
);


if (!target) throw new Error("Model is not available");


await session.updateModel({
  modelHandle: target.handle,
  reasoningEffort: "high",
});
```

`reasoningEffort` accepts `"none"`, `"minimal"`, `"low"`, `"medium"`, `"high"`, or `"xhigh"`, resolved against the model catalog. You can also pass `model` and `reasoningEffort` when creating or resuming a session; those updates persist on the agent.

## One-shot prompts

For scripts, smoke tests, and evals, `client.prompt()` sends one message and resolves with the turn’s result:

```
const result = await client.prompt("Reply with exactly: ok", agentId);
// → {
//   type: "result", success: true, result: "ok",
//   stopReason: "end_turn", durationMs: 1778,
//   conversationId: "conv-cd716204-…", runIds: ["run-71274347-…"]
// }
console.log(result.success, result.result);
// → true ok
```

Applications should use sessions.

## Read history

Read paginated conversation history with `listMessages()`:

```
const history = await session.listMessages({ order: "desc", limit: 20 });
// → {
//   messages: [
//     { id: "message-4eb205de-…", message_type: "assistant_message",
//       content: "The command printed: `hello-from-docs`.",
//       date: "2026-08-11T07:06:40.237Z", run_id: "run-52251ce8-…", … },
//     { id: "message-354a7295-…", message_type: "tool_return_message",
//       status: "success", tool_return: "hello-from-docs\n", … },
//     …
//   ],
//   …
// }
```

## Cleanup

Sessions implement `AsyncDisposable`. Use `await using` so the session closes when the scope exits, or call `close()` manually:

```
const session = client.createSession(agentId);
try {
  // ... use session ...
} finally {
  session.close();
}
```

## Advanced protocol commands

Most applications should use the typed SDK methods. For protocol-level integrations, `sendCommand()` sends raw App Server protocol commands; provide `responseType` when you want to wait for a protocol response. See the [SDK reference](/agent-sdk/reference/index.md) for the full session interface.

## What to read next

- [Sessions, turns, and durability](/agent-sdk/sessions/index.md) — what the SDK guarantees across connections
- [Permissions](/agent-sdk/permissions/index.md) — approving, denying, and editing tool calls
- [MCP and client tools](/agent-sdk/mcp/index.md) — defining the tools that appear in this stream
- [SDK reference](/agent-sdk/reference/index.md) — the full session interface
