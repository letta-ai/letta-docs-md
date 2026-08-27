---
title: Integration patterns | Letta Docs
description: Build robust Letta App Server controllers for custom UIs, teams, dashboards, and background orchestration
---

The recommended way to interface with the App Server is the [Letta Agent SDK](/agent-sdk/index.md), which provides a high-level interface over its WebSocket protocol.

Alternatively, use the App Server’s [OpenAI-compatible API](/platform/app-server/quickstart#openai-compatible-api/index.md) with clients such as Open WebUI, or the [ACP adapter](/platform/acp/index.md) with ACP clients such as Zed.

The Letta App Server is the runtime behind local and remote [Letta Agent SDK](/agent-sdk/index.md) sessions. Most applications should use the SDK; connect to App Server directly when your controller needs protocol-level runtime control.

Your controller should own product state and use App Server to run Letta agents. This page is written for agents and developers implementing direct controllers. Use it as a checklist before adding new protocol features.

## Choose the right surface

| Need                                                                     | Use                                                    |
| ------------------------------------------------------------------------ | ------------------------------------------------------ |
| High-level application API across managed, local, and remote deployments | [Letta Agent SDK](/agent-sdk/quickstart/index.md)      |
| Direct protocol control of a separately operated runtime                 | App Server client or protocol                          |
| Direct protocol control of a Letta-hosted remote environment             | [Remote client API](/agent-sdk/remote-client/index.md) |
| Direct server-side agent API without local computer-use tools            | [Letta API client SDKs](/v1-sdk/client-sdks/index.md)  |
| Human terminal workflow                                                  | Letta CLI                                              |
| Human workflow through an ACP-compatible client                          | [Agent Client Protocol (ACP)](/platform/acp/index.md)  |

Use the App Server client or protocol directly when you need to control runtime lifecycle, stream detailed events, or expose controller-owned tools beyond what the Agent SDK provides.

## Controller responsibilities

Keep these responsibilities in your application:

- Product objects, such as teams, tasks, projects, dashboards, and users
- Durable job state and results
- UI routing and optimistic state
- Reconnect logic and replay checkpoints
- Domain-specific authorization
- External API clients and secrets

Let App Server own these responsibilities:

- Resolving and creating Letta agents and conversations
- Running turns
- Preparing and executing local tools
- Managing runtime CWD and permission mode
- Streaming runtime events
- Routing external tool callbacks
- Replaying runtime state through `sync`

## Runtime registry pattern

Store runtime metadata in your controller database.

```
interface RuntimeRecord {
  id: string;
  agentId: string;
  conversationId: string;
  cwd: string | null;
  displayName: string;
  role: string;
  lastStartedAt: string;
}
```

On startup:

1. Load records from your database.
2. Start App Server.
3. For each active record, call `runtime_start` when you need that runtime.
4. Store the returned `runtime` exactly as App Server returns it.
5. Call `sync` before rendering stale UI state.

Do not rely on in-memory runtime state alone. App Server can restart, and a controller should be able to recover from its own database.

## Multi-agent orchestration pattern

For teams or agent pools, model each teammate as a persistent agent plus one or more conversations.

```
interface Teammate {
  name: string;
  role: string;
  agentId: string;
  defaultConversationId: string;
}


interface TaskRun {
  id: string;
  teammateName: string;
  conversationId: string;
  status: "queued" | "running" | "done" | "error";
  result?: string;
}
```

Use App Server for execution:

- `runtime_start` to start each teammate runtime
- `input` to dispatch work
- `stream_delta` to capture progress and results
- External tools like `update_task`, `complete_task`, or `dispatch_task` for structured coordination

Keep task state in the controller. Do not encode your full task database into agent memory or App Server runtime state.

## External tools as app commands

Prefer external tools for app-specific commands.

Good candidates:

- `dispatch_task`
- `update_progress`
- `complete_task`
- `lookup_ticket`
- `read_dashboard_state`
- `send_user_notification`

Avoid adding protocol commands for these unless multiple independent clients need the same primitive and the behavior belongs in the Letta agent harness.

## Reconnect and replay pattern

Websocket clients should be able to reconnect without losing their model of the world.

On reconnect:

1. Open a new `/ws` connection.
2. Call `runtime_start` for every runtime the connection should subscribe to.
3. Register connection-owned external tools again through each `runtime_start`.
4. Rebuild UI state from the automatic startup replay plus your durable controller state.
5. Call `sync` with `force_device_status: true` only when you need another explicit replay.

`runtime_start.external_tools` registrations belong to the connection and runtime. App Server removes them when that connection closes, so every replacement connection must register them again.

## Approval handling pattern

Decide early how your controller handles permission requests.

| Controller type          | Recommendation                                                                                                                                  |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Human-facing UI          | Render approval cards and answer with `input.kind: "approval_response"`                                                                         |
| Bot or background worker | Use a restrictive permission mode or tool allowlist                                                                                             |
| Trusted local automation | Use `acceptEdits` or `unrestricted` only when the environment is safe                                                                           |
| Multi-tenant service     | Keep App Server isolated per tenant or machine, require websocket auth for non-loopback listeners, and enforce authorization in your controller |

Do not leave background teammates waiting indefinitely on human approvals unless that is part of the product design.

## Tool visibility pattern

Use the smallest visibility surface that fits the task:

1. Omit `client_tool_allowlist` for normal agent harness behavior.
2. Use `client_tool_allowlist` to narrow built-in client tools for one turn.
3. Register unscoped external tools for safe controller actions that are always available.
4. Register scoped external tools and pass `external_tool_scope_ids` for context-specific abilities.

Do not use external tools as a security boundary by themselves. Treat them as model-facing visibility controls and enforce real authorization in the controller.

## Event handling pattern

Build event handlers as reducers. Store raw events when practical.

```
client.onMessage((message) => {
  appendEventLog({ message, receivedAt: Date.now() });


  switch (message.type) {
    case "stream_delta":
      updateTranscript(message.runtime, message.delta);
      break;
    case "update_loop_status":
      updateRuntimeStatus(message.runtime, message.loop_status);
      break;
    case "update_queue":
      replaceQueueSnapshot(message.runtime, message.queue);
      break;
    default:
      preserveUnknownEvent(message);
  }
});
```

Use tolerant parsing. New event fields and event types may appear as App Server evolves. Track `event_seq` independently for each connection when present, deduplicate events carrying an `idempotency_key`, and request `sync` when a sequence gap means the UI may have missed a state update.

## Concurrency pattern

App Server accepts multiple concurrent clients. Each connection can subscribe to multiple runtimes, and multiple connections can observe the same runtime without receiving events for unrelated subscriptions. Request correlation is connection-local, so different clients may safely reuse the same `request_id`.

Each `{agent_id, conversation_id}` should still have at most one active turn from your controller at a time.

Recommended controller behavior:

- Keep a per-runtime turn lock.
- Queue user messages while a runtime is active.
- Use `update_queue` and `update_loop_status` to reflect waiting/running state.
- Dispatch parallel work across different teammate runtimes, not the same conversation.
- Set clear timeouts around controller-owned external tools.

## When not to use App Server directly

Use the [Letta Agent SDK](/agent-sdk/quickstart/index.md) instead of integrating with the App Server protocol directly when you want a stable high-level abstraction and do not need protocol control. The SDK may still start or connect to App Server on your behalf.

A direct App Server integration is also the wrong surface when:

- You only need to create agents and send normal server-side messages through the Letta API.
- You need a public remote API exposed to browsers over the internet.
- You cannot run a trusted agent server in your environment.

For direct server-side agent operations without the App Server runtime, use the [Letta API client SDKs](/v1-sdk/client-sdks/index.md).

## Implementation checklist for agents

Before shipping an App Server integration:

- [ ] Start App Server on a loopback URL, or configure websocket auth for non-loopback listeners.
- [ ] Connect one bidirectional `/ws` socket.
- [ ] Read `app_server_info` and verify the server’s protocol version and capabilities.
- [ ] Treat every response and event on that socket as part of the protocol stream.
- [ ] Store canonical `runtime_start_response.runtime` values.
- [ ] Register external tools during every `runtime_start`.
- [ ] Keep product state outside App Server.
- [ ] Implement reconnect with `runtime_start` and `sync`.
- [ ] Add per-runtime turn locks.
- [ ] Decide approval behavior for background runs.
- [ ] Log unknown protocol events without crashing.
