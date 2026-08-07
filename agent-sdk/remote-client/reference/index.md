---
title: Remote client API reference | Letta Docs
description: Hosted environment discovery, authentication, relay channels, runtime startup, and reliability.
---

Use this reference after the [Remote client API overview](/agent-sdk/remote-client/index.md).

The Remote client API carries the [App Server protocol](/platform/app-server/protocol-lifecycle/index.md) through Letta’s hosted remote-environment router. This page documents the hosted transport around that shared protocol.

| Transport                 | Socket layout                                    | How the runtime is selected                                                           |
| ------------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------- |
| Direct App Server         | One bidirectional `/ws` connection               | Send `runtime_start` after connecting.                                                |
| Hosted remote environment | Two relay sockets labeled `control` and `stream` | Put the runtime IDs in both URLs, then send `runtime_start` on control by convention. |

## Hosted flow

1. List environments and choose an online `connectionId`.
2. Open both hosted relay channels for the agent and conversation.
3. Send `runtime_start` on control and store the canonical returned `runtime`.
4. Send commands on control by convention and consume events from both sockets.
5. ACK sequenced frames on the socket that delivered them.
6. Send heartbeats and recover state after event gaps or transport loss.

## Authentication

REST requests and Node/native WebSocket upgrades use the normal Letta API bearer token:

```
Authorization: Bearer $LETTA_API_KEY
```

Browser WebSocket APIs cannot set custom headers. Browser clients can add the token to each relay URL:

```
?token=<token>
```

Only use URL tokens over TLS, and do not log complete WebSocket URLs.

## Environment discovery

```
GET /v1/environments?onlineOnly=true
Authorization: Bearer $LETTA_API_KEY
```

Response

```
{
  "connections": [
    {
      "id": "env-...",
      "connectionId": "conn-...",
      "deviceId": "device-...",
      "connectionName": "Work laptop",
      "organizationId": "org-...",
      "connectedAt": 1780950000000,
      "lastHeartbeat": 1780950030000,
      "lastSeenAt": 1780950030000,
      "firstSeenAt": 1780940000000,
      "currentMode": "standard",
      "metadata": {
        "workingDirectory": "/workspace/project",
        "gitBranch": "main"
      }
    }
  ],
  "hasNextPage": false
}
```

`deviceId` is stable across reconnects. `connectionId` identifies the current online relay lease and can become `null` when the environment is offline. The lease is normally reused across transient reconnects, but may rotate after the environment re-registers.

You can also retrieve one environment by stable device ID:

```
GET /v1/environments/{deviceId}
Authorization: Bearer $LETTA_API_KEY
```

## Relay WebSockets

Open both channels:

```
wss://api.letta.com/v1/environments/{connectionId}/status/ws?agentId={agentId}&conversationId={conversationId}&channel=control
wss://api.letta.com/v1/environments/{connectionId}/status/ws?agentId={agentId}&conversationId={conversationId}&channel=stream
```

For browser query-token auth, append `&token={token}` to each URL.

| Parameter        | Meaning                                                                 |
| ---------------- | ----------------------------------------------------------------------- |
| `connectionId`   | Current online environment connection from the REST endpoint.           |
| `agentId`        | Persistent Letta agent ID.                                              |
| `conversationId` | Conversation ID, or `default` for the agent’s default conversation.     |
| `channel`        | Client-side label used by the SDK to distinguish its two relay sockets. |
| `token`          | Browser-only authentication fallback when headers are unavailable.      |

The client should wait for both sockets before starting the runtime. The current endpoint subscribes both sockets to the same event feed and accepts commands from either; it does not enforce control-only commands or stream-only events. The SDK sends commands on control and filters duplicate delivery client-side.

Custom clients must consume both sockets, correlate direct responses by `request_id`, and ignore a response when that request has already resolved. This matters because direct responses such as `runtime_start_response` may be delivered on both sockets and do not necessarily include an `idempotency_key`.

## Runtime startup

Send `runtime_start` on control after the two WebSockets open:

runtime\_start

```
{
  "type": "runtime_start",
  "request_id": "runtime-1",
  "agent_id": "agent-...",
  "conversation_id": "conv-...",
  "cwd": "/workspace/project",
  "mode": "standard",
  "recover_approvals": false,
  "force_device_status": true,
  "client_info": {
    "name": "my_client",
    "title": "My client",
    "version": "1.0.0"
  }
}
```

runtime\_start\_response

```
{
  "type": "runtime_start_response",
  "request_id": "runtime-1",
  "success": true,
  "runtime": {
    "agent_id": "agent-...",
    "conversation_id": "conv-..."
  },
  "created": {
    "agent": false,
    "conversation": false
  },
  "agent": {},
  "conversation": {}
}
```

Use the returned `runtime` on later scoped commands. `runtime_start` also applies runtime options, registers external tools when provided, and emits the initial state replay.

## Frame shape

Every relay frame is a JSON object with a `type` field.

| Field                     | Direction       | Meaning                                                    |
| ------------------------- | --------------- | ---------------------------------------------------------- |
| `type`                    | Both            | Discriminates commands, responses, and events.             |
| `request_id`              | Both            | Correlates and deduplicates direct responses.              |
| `runtime.agent_id`        | Both            | Persistent agent in the runtime scope.                     |
| `runtime.conversation_id` | Both            | Conversation in the runtime scope.                         |
| `seq`                     | Relay → client  | Per-socket delivery sequence. ACK it on the same socket.   |
| `event_seq`               | Device → client | Device event ordering across relay delivery.               |
| `idempotency_key`         | Device → client | Stable key on events that support transport deduplication. |

## Transport acknowledgements

When either socket receives a frame containing `seq`, reply on that same socket:

```
{ "type": "ack", "seq": 42 }
```

The ACK has no direct response. It is relay bookkeeping, not confirmation that a runtime command succeeded.

## Heartbeats

Send an application-level ping on both sockets every 30 seconds:

```
{ "type": "ping" }
```

Each healthy channel responds with `pong`. If either channel closes, close the other and reconnect the pair rather than continuing with a partial transport.

## Shared command lifecycle

After startup, use the canonical App Server protocol for runtime operations:

| Task                                                                   | Canonical docs                                                                                                          |
| ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Send a user turn                                                       | [`input` with `payload.kind: "create_message"`](/platform/app-server/protocol-lifecycle#sending-turns/index.md)         |
| Respond to approvals                                                   | [`input` with `payload.kind: "approval_response"`](/platform/app-server/protocol-lifecycle#approval-responses/index.md) |
| Replay state                                                           | [`sync`](/platform/app-server/protocol-lifecycle#sync/index.md)                                                         |
| Abort active work                                                      | [`abort_message`](/platform/app-server/protocol-lifecycle#abort/index.md)                                               |
| Handle output and runtime state                                        | [Streaming and completion](/platform/app-server/protocol-lifecycle#streaming-and-completion/index.md)                   |
| Use filesystem, memory, model, terminal, schedule, or channel commands | [Management and computer commands](/platform/app-server/protocol-lifecycle#management-and-computer-commands/index.md)   |

The protocol is a discriminated-union event stream, not JSON-RPC. Preserve unknown fields and log unknown event types instead of crashing.

## Remote-specific responses

| Send            | Receive                           | Notes                                                                |
| --------------- | --------------------------------- | -------------------------------------------------------------------- |
| `runtime_start` | `runtime_start_response`          | Correlate by `request_id`; store the returned runtime.               |
| `ping`          | `pong`                            | Send independently on both relay channels.                           |
| `ack`           | No direct response                | Acknowledges one channel’s transport `seq`.                          |
| `sync`          | `sync_response` plus state events | Replay events can arrive after the correlated response.              |
| `abort_message` | `abort_message_response`          | Correlate by `request_id`; later status events remain authoritative. |

## Recovery and deduplication

- Track `event_seq`. If it advances by more than one, send `sync` with `recover_approvals: true` and `force_device_status: true`.
- Keep a bounded set of `idempotency_key` values and drop duplicate events.
- Track resolved `request_id` values so duplicate direct responses are ignored even when they have no `idempotency_key`.
- Acknowledge `seq` before applying higher-level event handling.
- If either socket disconnects, close the pair. For raw clients, resolve the current lease, open a fresh pair, and send `runtime_start`; it performs the initial state replay.
- The Agent SDK does not reconnect an existing session. Create a fresh `resumeSession(...)` and call `recoverPendingApprovals()` if explicit approval recovery is needed.
- Treat `stream_delta.delta.message_type: "stop_reason"` as normal turn completion.
- Treat `stream_delta.delta.message_type` values `loop_error` and `error_message`, plus top-level `error` and `run_request_error` frames, as failures.

## Related pages

- [Remote client API overview](/agent-sdk/remote-client/index.md) - Hosted flow and a minimal transport example.
- [Self-hosting](/self-hosting/index.md) - Run local agents on infrastructure you control and connect through App Server.
- [App Server protocol lifecycle](/platform/app-server/protocol-lifecycle/index.md) - Canonical runtime commands and events.
