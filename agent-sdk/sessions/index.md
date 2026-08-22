---
title: Sessions, turns, and durability | Letta Docs
description: The agent, conversation, and session model, and what the SDK guarantees across connections
---

An **agent** is the persistent entity with memory. A **conversation** is a thread on that agent. A **session** is the active connection you use to send messages and stream events.

- Agent IDs look like `agent-xxx` on the cloud backend and `agent-local-xxx` on the local backend. Conversation IDs look like `conv-xxx`.
- `createAgent()` also creates the agent’s default conversation, so a new agent is immediately usable.
- `createSession(agentId)` starts a **new** conversation on an existing agent.
- `resumeSession(id)` accepts either kind of ID: pass an `agent-xxx` ID to resume the agent’s default conversation, or a `conv-xxx` ID to resume a specific conversation.

```
// New conversation on an existing agent
await using session = client.createSession(agentId);


// Later: save the thread and pick it up again
const conversationId = session.conversationId;
// → "conv-cff81390-0763-431d-b24e-b218ae37ec81"
await using resumed = client.resumeSession(conversationId);


// Or resume the agent's default conversation
await using main = client.resumeSession(agentId);
```

Sessions expose read-only `agentId`, `conversationId`, and `sessionId` values once the backend resolves them (`sessionId` is `"<agentId>:<conversationId>"`). You can also create and inspect conversations without opening a session through `client.conversations` (`create`, `list`, `retrieve`, `update`, `listMessages`).

## Anatomy of a turn

A turn is one `send()` plus one pass through `stream()`:

1. `send()` transmits the user message (or queues it if a turn is already streaming — the runtime owns the queue).
2. `stream()` yields the turn’s typed events — reasoning, tool calls, tool results, assistant text — and **terminates after the turn’s `result` message**.
3. The `result` carries the turn’s full final text, `success`, `stopReason`, and `durationMs`. Its `runIds` field lists the Letta runs started by the turn.

See [Sending messages](/agent-sdk/messages/index.md) for the full event contract with captured payloads.

## Interruption and cleanup

- `abort()` requests cancellation of the active turn without closing the session. Continue consuming the stream until its terminal `result`.
- `close()` (or `await using` disposal) releases the session and its local resources: MCP connections, client tools, and any session-scoped repository `resources` links.
- A session whose connection closed unexpectedly **cannot be reused**. The stream emits an `error` followed by a failed `result`; call `resumeSession(conversationId)` to continue in a new session.

## What persists, and what doesn’t

| Persists beyond one SDK connection                        | Scoped to the SDK session                                                         |
| --------------------------------------------------------- | --------------------------------------------------------------------------------- |
| The agent’s memory and conversation history               | [Client tools and MCP servers](/agent-sdk/mcp/index.md)                           |
| `model` and `reasoningEffort` updates passed to sessions  | `canUseTool` callbacks and [permission](/agent-sdk/permissions/index.md) behavior |
| Persistent repository attachments (`agents.repositories`) | Session `resources` repository links                                              |
| Pending approvals while the runtime remains active        | `cwd`, `env`, and computer or sandbox selection                                   |

## Run a turn without touching memory

Pass `stateless: true` to run a session that does not load or change the agent’s [memory](/agent-sdk/memory/index.md). The agent and the conversation are still persistent — only this session’s memory, agent skills, agent mods, transcript, and reflection behavior change:

```
await using session = client.resumeSession(agentId, { stateless: true });
```

Use it for a one-off turn you do not want shaping the agent’s long-term memory.

## Guarantees and non-guarantees

- **Messages you `send()` while a turn is active are queued by the runtime**, not dropped; `stream()` may emit `queue_update` events, and `removeQueuedMessage(itemId)` waits for the authoritative queue response.
- **A pending approval can remain on an active runtime after a client disconnects.** After you resume the session, check `getDeviceStatus()` and follow [Recover pending approvals](/agent-sdk/permissions#recover-pending-approvals/index.md).
- **The SDK does not replay events missed while disconnected.** After resuming, reconcile with `listMessages()` or fetch a consolidated snapshot with `bootstrapState()`. If you merge fetched history while a turn is still streaming, rebase any in-progress accumulators onto it — see [Message identity](/agent-sdk/messages#message-identity/index.md).
- **If a connection fails after `send()` succeeded, do not blindly retry** — the message may already have reached the runtime. Inspect the conversation history first. The one automatic retry the docs recommend is the pre-send `CloudManagedSandboxExpiredError` case in [Deployment](/agent-sdk/deployment#recover-from-an-expired-sandbox/index.md).
- **Run IDs connect stream messages to Letta runs.** `assistant`, `reasoning`, `tool_call`, `tool_result`, `error`, and `retry` messages include `runId` when they belong to a run. The final `result.runIds` lists all runs started by the turn. If the turn fails before the runtime starts a run, `result.runIds` is absent.

## What to read next

- [Sending messages](/agent-sdk/messages/index.md) — the full stream event contract
- [Permissions](/agent-sdk/permissions/index.md) — interactive approvals and recovery
- [Creating agents](/agent-sdk/agents/index.md) — memory and agent configuration
- [SDK reference](/agent-sdk/reference/index.md) — the complete session interface
