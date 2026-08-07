---
title: Protocol lifecycle | Letta Docs
description: Understand the Letta App Server WebSocket connection, runtime_start, input, sync, abort, and event handling
---

The recommended way to interface with the App Server is the [Letta Agent SDK](/agent-sdk/index.md), which provides a high-level interface over its WebSocket protocol.

Alternatively, use the App Server’s [OpenAI-compatible API](/platform/app-server/quickstart#openai-compatible-api/index.md) with clients such as Open WebUI, or the [ACP adapter](/platform/acp/index.md) with ACP clients such as Zed.

The Letta App Server uses one bidirectional WebSocket. Every command, response, and event is a JSON object with a `type` field. Commands that expect a direct response include a `request_id`; runtime events include sequencing and idempotency metadata.

This is the canonical lifecycle reference for the shared App Server command and event model. The [Remote client API](/agent-sdk/remote-client/reference/index.md) uses the same frame vocabulary over a hosted remote-environment transport, but adds environment discovery, authentication, relay connections, and delivery acknowledgements.

## Transport

Start App Server:

Terminal window

```
letta server --listen ws://127.0.0.1:4500
```

The process prints one WebSocket endpoint:

```
Listening on ws://127.0.0.1:4500
WebSocket: ws://127.0.0.1:4500/ws
```

Open one connection to `/ws`. Send every command and receive every response, approval, tool callback, streamed delta, and state update on that socket. App Server rejects the legacy `?channel=control` and `?channel=stream` layout with HTTP 426.

Loopback listeners do not require authentication. A non-loopback listener refuses to start unless you configure `--ws-auth capability-token` or `--ws-auth signed-bearer-token`; native clients send the credential as `Authorization: Bearer ...` during the WebSocket upgrade.

App Server accepts `ws://` listen URLs. Terminate TLS at a reverse proxy when clients connect over `wss://`. The standard browser WebSocket API cannot set the required `Authorization` header, so authenticated browser applications need a trusted backend or WebSocket proxy.

HTTP requests carrying an `Origin` header are rejected. An Origin-bearing WebSocket upgrade is accepted only when App Server authentication is configured and the native client also sends valid authorization.

The server exposes these unauthenticated, no-origin health probes:

| Endpoint       | Result                                         |
| -------------- | ---------------------------------------------- |
| `GET /readyz`  | `200 OK` when the listener accepts connections |
| `GET /healthz` | `200 OK` while the process is healthy          |

## Capability discovery

Before relying on optional protocol features, read App Server’s version and capabilities over HTTP:

```
GET /app-server-info
Authorization: Bearer <token>
```

When authentication is enabled, this endpoint requires the same bearer token as the WebSocket. You can also request the information after connecting:

```
{ "type": "app_server_info", "request_id": "info-1" }
```

The `app_server_info_response` includes the Letta Code version, numeric protocol version, active backend, and capability flags such as `runtime_start` and `split_channels`. Current App Server versions report `split_channels: false`.

## Connections and runtime subscriptions

App Server accepts multiple concurrent WebSocket clients. Each connection has independent request correlation, runtime subscriptions, event sequencing, external tools, approvals, and terminal processes.

`runtime_start` subscribes the sending connection to the returned `{agent_id, conversation_id}` scope. One connection can subscribe to multiple runtimes, and multiple connections can subscribe to the same runtime. Runtime-scoped events are delivered only to subscribed connections; disconnecting one client does not close the others.

## Runtime startup

Send `runtime_start` before sending turns. It resolves the agent and conversation, applies runtime state, registers external tools, and replays state.

runtime\_start

```
{
  "type": "runtime_start",
  "request_id": "runtime-1",
  "agent_id": "agent-123",
  "conversation_id": "conv-123",
  "cwd": "/Users/me/project",
  "mode": "standard",
  "client_info": {
    "name": "my_app",
    "title": "My App",
    "version": "0.1.0"
  },
  "recover_approvals": true,
  "force_device_status": true
}
```

The response contains the canonical runtime scope:

runtime\_start\_response

```
{
  "type": "runtime_start_response",
  "request_id": "runtime-1",
  "success": true,
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "created": {
    "agent": false,
    "conversation": false
  },
  "agent": {},
  "conversation": {}
}
```

Use the returned `runtime` for all scoped commands. Do not reconstruct it from assumptions if App Server created either object.

## Creating agents and conversations

`runtime_start` accepts exactly one of `agent_id` or `create_agent`.

Create an agent

```
{
  "type": "runtime_start",
  "request_id": "runtime-1",
  "create_agent": {
    "body": {
      "name": "Build Agent",
      "memory_blocks": []
    },
    "pin_global": true
  },
  "create_conversation": {
    "body": {}
  }
}
```

Pass an existing `conversation_id` to resume that conversation. If you omit it, App Server creates a conversation for the resolved agent; `create_conversation.body` optionally supplies its creation fields. The special conversation ID `default` selects the agent’s virtual default conversation.

## Runtime state fields

| Field                 | Direction                              | Meaning                                                                          |
| --------------------- | -------------------------------------- | -------------------------------------------------------------------------------- |
| `cwd`                 | `runtime_start`, `change_device_state` | Working directory for local tools. `null` resets to the listener boot directory. |
| `mode`                | `runtime_start`, `change_device_state` | Permission mode for local tool execution.                                        |
| `skill_sources`       | `runtime_start`                        | Skill sources available to the resolved runtime.                                 |
| `recover_approvals`   | `runtime_start`, `sync`                | Probe backend state for stale pending approvals. Defaults to `true`.             |
| `force_device_status` | `runtime_start`, `sync`                | Force a device status replay even if the cached status did not change.           |
| `client_info`         | `runtime_start`                        | Client metadata for diagnostics and future negotiation.                          |
| `external_tools`      | `runtime_start`                        | Controller-owned tools registered for this connection and runtime.               |

Valid permission modes are `standard`, `acceptEdits`, `unrestricted`, and `strict`.

## Sending turns

Use `input` with `payload.kind: "create_message"` to send a user turn.

input create\_message

```
{
  "type": "input",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "payload": {
    "kind": "create_message",
    "messages": [
      {
        "role": "user",
        "content": "Inspect the auth flow and report risks.",
        "client_message_id": "client-msg-1"
      }
    ],
    "client_tool_allowlist": ["Read", "Grep", "Glob"]
  }
}
```

`client_message_id` is optional, but useful for UI deduplication and local optimistic rows.

`client_tool_allowlist` narrows the locally executed client tools for this turn. Omit it to use the runtime’s normal toolset. Pass an empty array to expose no client tools for the turn.

Use `external_tool_scope_ids` to expose scoped controller tools registered by `runtime_start`. Set `exclude_interactive_tools: true` for headless clients that cannot surface mid-turn questions to a person.

## Approval responses

Use `input` with `payload.kind: "approval_response"` to answer a pending approval request.

Allow a tool call

```
{
  "type": "input",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "payload": {
    "kind": "approval_response",
    "request_id": "approval-123",
    "decision": {
      "behavior": "allow",
      "message": "Approved by controller"
    }
  }
}
```

Deny a tool call

```
{
  "type": "input",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "payload": {
    "kind": "approval_response",
    "request_id": "approval-123",
    "decision": {
      "behavior": "deny",
      "message": "Do not modify production files"
    }
  }
}
```

## Streaming and completion

The primary turn event is `stream_delta`:

stream\_delta

```
{
  "type": "stream_delta",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "event_seq": 42,
  "emitted_at": "2026-07-31T18:00:00.000Z",
  "idempotency_key": "stream_delta:42:550e8400-e29b-41d4-a716-446655440000",
  "delta": {
    "id": "msg-1",
    "date": "2026-06-17T00:00:00.000Z",
    "message_type": "status",
    "message": "Reading files",
    "level": "info"
  }
}
```

A turn is complete when a `stream_delta` carries `delta.message_type: "stop_reason"`, except for `stop_reason: "requires_approval"`. Approval is a continuation boundary: keep the runtime active, render the matching `control_request`, and send an approval response. Treat `loop_error` and `error_message` deltas as failures.

Also handle runtime and controller events:

| Event                        | Use                                                   |
| ---------------------------- | ----------------------------------------------------- |
| `control_request`            | Pending permission request                            |
| `external_tool_call_request` | Controller-owned tool callback                        |
| `update_loop_status`         | Active run IDs and waiting/running state              |
| `update_device_status`       | Runtime availability, cwd, mode, and status snapshots |
| `update_queue`               | Full turn queue snapshot                              |
| `update_subagent_state`      | Subagent state snapshots                              |
| `stream_delta`               | Agent output and lifecycle deltas                     |

All events arrive on the same WebSocket. Route scoped events by `runtime`, correlate direct responses by `request_id`, and process increasing `event_seq` values per connection when present. Use `idempotency_key` to deduplicate replayed or retried events. Preserve unknown fields and event types so clients remain forward-compatible.

## Sync

A successful `runtime_start` automatically replays the subscribed runtime’s current state after its response. Use `sync` on an established connection when a UI needs another replay or explicit pending-approval recovery.

sync

```
{
  "type": "sync",
  "request_id": "sync-1",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "recover_approvals": false,
  "force_device_status": true
}
```

The replayed state arrives as normal events. App Server sends `sync_response` after the replay succeeds or returns an error if the replay fails.

sync\_response

```
{
  "type": "sync_response",
  "request_id": "sync-1",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "success": true
}
```

After transport loss, open a new WebSocket and send `runtime_start` again to restore subscriptions and connection-owned external tools. Disconnect cleanup removes that connection’s pending approvals, tool callbacks, terminals, and queued input. If no other subscribed client can take over an active runtime, App Server requests cancellation of its active turn.

## Abort

Use `abort_message` to stop active work or interrupt a pending approval.

abort\_message

```
{
  "type": "abort_message",
  "request_id": "abort-1",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  }
}
```

abort\_message\_response

```
{
  "type": "abort_message_response",
  "request_id": "abort-1",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "aborted": true,
  "success": true
}
```

## Management and computer commands

App Server exposes the same management and computer capabilities used by Letta’s own clients. Current command groups include:

- App Server capability discovery
- Agent and conversation creation, retrieval, updates, deletion, forking, message listing, and compaction
- Filesystem, content search, and git branch operations
- Memory files, history, commit diffs, and MemFS enablement
- Models, providers, toolsets, experiments, and reflection settings
- Skills and secrets
- Terminals and command execution
- Schedules and run history
- Channels, accounts, routes, targets, and pairings

Use `request_id` on commands that return a response. TypeScript clients can import the current `WsProtocolCommand` and `WsProtocolMessage` unions from `@letta-ai/letta-code/app-server-protocol` instead of copying a command list. Keep handlers tolerant of additional fields and unknown message types.

## Legacy command names to avoid

Do not use these legacy listener command names in new App Server clients:

| Do not send                 | Use instead                               |
| --------------------------- | ----------------------------------------- |
| `request_state`             | `sync`                                    |
| `change_cwd`                | `change_device_state` with `payload.cwd`  |
| `change_mode`               | `change_device_state` with `payload.mode` |
| `cancel_run`                | `abort_message`                           |
| `recover_pending_approvals` | `sync` with `recover_approvals: true`     |
