---
title: Letta Agent SDK quickstart | Letta Docs
description: Learn the basics of the SDK
---

## Quickstart

Use the Agent SDK to build stateful agents for applications, from personal assistants to digital employees. Create an agent, start a session, and stream its response with JavaScript or TypeScript.

Python applications must use the [App Server WebSocket protocol](/platform/app-server/protocol-lifecycle/index.md) directly.

- [Managed cloud](#tab-panel-0)
- [Local](#tab-panel-1)
- [Remote server](#tab-panel-2)

1. **Get an API key**

   Create an API key from [platform.letta.com/api-keys](https://platform.letta.com/api-keys) and set it as an environment variable:

   ```
   export LETTA_API_KEY='your-api-key-here'
   ```

2. **Install the SDK**

   ```
   npm install @letta-ai/letta-agent-sdk tsx
   ```

3. **Create your code**

   Save this as `quickstart.ts`:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   async function main() {
     const client = new LettaAgentClient({
       backend: "cloud",
       apiKey: process.env.LETTA_API_KEY,
     });


     const agentId = await client.createAgent({
       model: "anthropic/claude-opus-4-8",
       persona:
         "You are Nora, a proactive digital chief of staff. You research, write crisp briefs, remember preferences, and turn ambiguous requests into concrete next steps.",
       human:
         "The user wants concise executive summaries, explicit risks, and suggested follow-up actions.",
     });


     await using session = client.createSession(agentId);


     console.log("Agent ID:", agentId);


     await session.send(
       "Research the launch plan for a small SDK release. Draft a status brief, list the top risks, and propose the first three follow-up tasks.",
     );


     let printedConversationId = false;
     for await (const message of session.stream()) {
       if (!printedConversationId && session.conversationId) {
         console.log("Conversation ID:", session.conversationId);
         printedConversationId = true;
       }
       if (message.type === "assistant") {
         console.log(message.content);
       }
     }
   }


   main().catch((error) => {
     console.error(error);
     throw error;
   });
   ```

4. **Run your code**

   ```
   npx tsx quickstart.ts
   ```

5. **Example output**

   ```
   Agent ID: agent-abc123
   Conversation ID: conv-abc123
   ## SDK release brief
   - Current state: ...
   - Risks: ...
   - Follow-ups: ...
   ```

Use [shared memory repositories](/agent-sdk/repositories/index.md) to give Cloud agents versioned files. Attach a repository for one session or keep it attached to the agent.

1. **Install Node.js**

   The SDK runs Letta Code locally as a subprocess. Install [Node.js](https://nodejs.org/en/download) version 22.19+.

2. **Install the SDK**

   ```
   npm install @letta-ai/letta-agent-sdk tsx
   ```

3. **Create your code**

   Save this as `quickstart.ts`:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   async function main() {
     const client = new LettaAgentClient({ backend: "local" });


     const agentId = await client.createAgent({
       persona:
         "You are Patch, a resident engineering teammate for this repository. You inspect files before changing them, learn local conventions, and keep a memory of durable codebase patterns.",
       human:
         "The user prefers practical handoffs: architecture notes, commands to run, and gotchas worth remembering.",
     });


     await using session = client.createSession(agentId, {
       cwd: process.cwd(),
     });


     console.log("Agent ID:", agentId);


     await session.send(
       "Inspect this repository and write an onboarding memo for a new engineer: architecture, important workflows, and gotchas.",
     );


     let printedConversationId = false;
     for await (const message of session.stream()) {
       if (!printedConversationId && session.conversationId) {
         console.log("Conversation ID:", session.conversationId);
         printedConversationId = true;
       }
       if (message.type === "assistant") {
         console.log(message.content);
       }
     }
   }


   main().catch((error) => {
     console.error(error);
     throw error;
   });
   ```

4. **Run your code**

   ```
   npx tsx quickstart.ts
   ```

5. **Example output**

   ```
   Agent ID: agent-abc123
   Conversation ID: conv-abc123
   ## Engineering onboarding memo
   - Architecture: ...
   - Workflows: ...
   - Gotchas: ...
   ```

1) **Start an App Server**

   To keep agent state and the execution environment on the App Server machine, start it with the local backend:

   ```
   letta server --backend local --listen ws://127.0.0.1:4500
   ```

   App Server can also use the cloud backend when you want the execution environment on this machine while agent state remains hosted in Letta Cloud. See [App Server](/platform/app-server/index.md) for deployment and authentication options.

2) **Install the SDK**

   ```
   npm install @letta-ai/letta-agent-sdk tsx
   ```

3) **Create your code**

   Save this as `quickstart.ts`:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   async function main() {
     const client = new LettaAgentClient({
       backend: "remote",
       url: process.env.LETTA_APP_SERVER_URL ?? "http://127.0.0.1:4500",
       authToken: process.env.LETTA_APP_SERVER_TOKEN,
     });


     const agentId = await client.createAgent({
       persona:
         "You are Ops, a digital employee running in a shared workspace. You use shell and file tools to inspect systems, prepare handoff reports, and coordinate follow-up work.",
       human:
         "The user values morning briefs with evidence, blockers, owners, and suggested next actions.",
     });


     await using session = client.createSession(agentId, {
       cwd: "/workspace/project",
     });


     console.log("Agent ID:", agentId);


     await session.send(
       "Prepare a morning handoff report: inspect the workspace, summarize recent changes, identify blockers, and list the first actions you recommend.",
     );


     let printedConversationId = false;
     for await (const message of session.stream()) {
       if (!printedConversationId && session.conversationId) {
         console.log("Conversation ID:", session.conversationId);
         printedConversationId = true;
       }
       if (message.type === "assistant") {
         console.log(message.content);
       }
     }
   }


   main().catch((error) => {
     console.error(error);
     throw error;
   });
   ```

4) **Run your code**

   ```
   LETTA_APP_SERVER_URL='http://127.0.0.1:4500' npx tsx quickstart.ts
   ```

5) **Example output**

   ```
   Agent ID: agent-abc123
   Conversation ID: conv-abc123
   ## Morning handoff
   - Recent changes: ...
   - Blockers: ...
   - Recommended actions: ...
   ```

## Browser and React Native

Use the portable `/client` entry point in browser, Expo, and React Native applications. It includes the Cloud and Remote transports without importing Node process-management modules.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk/client";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: userProvidedApiKey,
  webSocketAuth: "query",
});
```

The portable entry point supports `backend: "cloud"` and `backend: "remote"`. Import from the package root when you need `backend: "local"`, which starts and manages a local App Server process.

Browser WebSockets cannot set upgrade headers, so Cloud clients should use `webSocketAuth: "query"`. For an authenticated Remote App Server in React Native, adapt the platform WebSocket constructor:

```
import {
  LettaAgentClient,
  createReactNativeWebSocketConstructor,
} from "@letta-ai/letta-agent-sdk/client";


const client = new LettaAgentClient({
  backend: "remote",
  url: appServerUrl,
  authToken: appServerToken,
  WebSocket: createReactNativeWebSocketConstructor(WebSocket),
});
```

## Sessions

An agent is the persistent entity with memory. A conversation is a thread on that agent. A session is the active connection you use to send messages and stream events.

### Start a new conversation

Use `createSession(agentId)` when you want a new conversation on an existing agent.

```
const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  persona:
    "You are Avery, a persistent product operations partner who remembers context, writes plans, and follows through across conversations.",
});


await using session = client.createSession(agentId);


await session.send(
  "Plan next week's beta launch: milestones, owner checklist, open questions, and a concise Slack update.",
);
let printedConversationId = false;
for await (const message of session.stream()) {
  if (!printedConversationId && session.conversationId) {
    console.log("Save this conversation ID:", session.conversationId);
    printedConversationId = true;
  }
  if (message.type === "assistant") console.log(message.content);
}
```

### Resume a conversation

Save `session.conversationId` and pass it to `resumeSession()` later.

```
const conversationId = "conv-abc123";


await using session = client.resumeSession(conversationId);


await session.send("Continue from where we left off.");
for await (const message of session.stream()) {
  if (message.type === "assistant") console.log(message.content);
}
```

### Resume the main conversation

Each agent also has a main conversation. Pass an `agentId` to `resumeSession()` to resume that default thread.

```
await using session = client.resumeSession(agentId);
```

## Interaction

### Stream a turn

Use `send()` to start a turn and `stream()` to read events until the result message.

```
await session.send("Run the tests and summarize the failures.");


for await (const message of session.stream()) {
  if (message.type === "reasoning") {
    console.log("thinking:", message.content);
  }


  if (message.type === "tool_call") {
    console.log("tool:", message.toolName, message.toolInput);
  }


  if (message.type === "assistant") {
    console.log(message.content);
  }


  if (message.type === "queue_update") {
    console.log("queued turns:", message.queue.length);
  }


  if (message.type === "result" && !message.success) {
    console.error(message.errorDetail ?? message.error);
  }
}
```

Cloud, Remote, and Local agent sessions can accept another `send()` while a turn is streaming. The listener owns queueing and `stream()` may emit `queue_update` events before the current turn’s `result`.

### Handle permission requests

Use `canUseTool` to approve, deny, or edit tool calls. The callback can be fully interactive: return a promise that resolves after your UI or server receives a user’s decision. The SDK keeps the tool approval pending until the callback returns. This example asks the agent to run a shell command and denies the `Bash` tool call so you can see the callback fire.

```
await using session = client.createSession(agentId, {
  permissionMode: "standard",
  canUseTool: async (toolName, toolInput) => {
    console.log("approval requested:", toolName, toolInput);


    if (toolName === "Bash") {
      return {
        behavior: "deny",
        message: "Denied by the example approval policy",
      };
    }


    return { behavior: "allow" };
  },
});


await session.send("Use Bash to run exactly: echo permission-check");


for await (const message of session.stream()) {
  if (message.type === "tool_call") {
    console.log("tool:", message.toolName, message.toolInput);
  }


  if (message.type === "tool_result") {
    console.log("tool result:", message.content);
  }


  if (message.type === "assistant") {
    console.log(message.content);
  }


  if (message.type === "result") break;
}
```

`permissionMode: "unrestricted"` auto-allows tool calls that do not require user input. Tools that ask the user for input still flow through `canUseTool`, so your app can render the prompt and return the user’s response.

### Interrupt a turn

Call `abort()` to stop the active turn without closing the session.

```
await session.send("Run the full test suite and fix failures.");


setTimeout(() => {
  void session.abort();
}, 5_000);


for await (const message of session.stream()) {
  if (message.type === "result") break;
}
```

Use `close()` when you are done with the SDK session and want to release its resources.

### Change model and reasoning effort

Inspect the model catalog and update the model between turns when you want to trade speed, cost, and reasoning depth.

```
const catalog = await session.listModels();
const target = catalog.entries.find(
  (entry) => entry.handle === "anthropic/claude-opus-4-8",
);


if (!target) throw new Error("Model is not available");


await session.updateModel({
  modelHandle: target.handle,
  reasoningEffort: "high",
});


await session.send("Use the stronger model to pressure-test the launch risks.");
```

`reasoningEffort` is resolved against the model catalog. Use a model ID returned by `listModels()` or a full `modelHandle`; avoid shorthand names unless they are real catalog IDs. You can also pass `model` and `reasoningEffort` when creating or resuming a session.

### Send advanced protocol commands

Most applications should use the typed SDK methods. For protocol-level integrations, use `sendCommand()` with raw Letta Code websocket protocol commands.

```
if (!session.agentId || !session.conversationId) {
  throw new Error("Session is not initialized");
}


const runtime = {
  agent_id: session.agentId,
  conversation_id: session.conversationId,
};


await session.sendCommand({
  type: "change_device_state",
  runtime,
  payload: { cwd: "/workspace/project" },
});


const sync = await session.sendCommand<{
  type: "sync_response";
  success: boolean;
}>({ type: "sync", runtime }, { responseType: "sync_response" });


console.log("Synced:", sync.success);
```

Omit `responseType` for fire-and-forget commands. Provide `responseType` or a custom predicate when you want to wait for a protocol response.

## Configuration

### Agent options

Configure persistent agent state when you call `createAgent()`.

```
const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  persona:
    "You are Quinn, a digital research analyst who can inspect files, run commands, synthesize sources, and maintain living memory about the user's organization.",
  human:
    "The user prefers concise memos with evidence, caveats, and recommended next actions.",
});
```

You can also pass memory blocks directly:

```
const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  memory: [
    {
      label: "persona",
      value:
        "You are Quinn, a digital research analyst who can inspect files, run commands, synthesize sources, and maintain living memory about the user's organization.",
    },
    {
      label: "human",
      value:
        "The user prefers concise memos with evidence, caveats, and recommended next actions.",
    },
  ],
});
```

### Session options

Configure runtime behavior when you call `createSession(agentId, options)` or `resumeSession(id, options)`: model, reasoning effort, current working directory, and permission mode.

```
await using session = client.createSession(agentId, {
  cwd: "/path/to/project",
  model: "anthropic/claude-opus-4-8",
  reasoningEffort: "medium",
  permissionMode: "standard",
});
```

| Setting                             | Option            |
| ----------------------------------- | ----------------- |
| Model                               | `model`           |
| Reasoning effort                    | `reasoningEffort` |
| Working directory                   | `cwd`             |
| Permission mode                     | `permissionMode`  |
| Interactive approvals and questions | `canUseTool`      |

For Cloud and Remote sessions, `cwd` must be a path inside the selected runtime environment, not a local path on the SDK caller’s machine.

`model` updates passed to `createSession(agentId, options)` or `resumeSession(id, options)` persist on the agent.

### System prompts

Keep the default system prompt for most agents. It includes the instructions that teach the agent how to use the harness, including tools and memory. Customize `persona`, `human`, and [MemFS](/concepts/memfs/index.md) instead.

Set `systemPrompt` only when your application needs a deliberately different operating model, such as a companion or another specialized environment:

```
const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  systemPrompt:
    "You are a highly autonomous digital employee. Use tools to gather evidence, write concise reports, and remember durable preferences.",
});
```

Preset names include `default`, `letta-claude`, `letta-codex`, `letta-gemini`, `claude`, `codex`, and `gemini`, but `createAgent()` currently accepts custom system prompt strings, not preset names.

### Cleanup

Sessions can be closed automatically with `await using` or manually with `session.close()`.

```
const session = client.createSession(agentId);
try {
  // ... use session ...
} finally {
  session.close();
}
```

For client methods, session types, and option interfaces, see the [SDK reference](/agent-sdk/reference/index.md).
