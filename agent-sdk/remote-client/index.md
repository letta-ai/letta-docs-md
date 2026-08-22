---
title: Remote client API | Letta Docs
description: Low-level hosted transport for custom clients that control Letta Code remote environments.
---

The Remote client API connects a custom client to a Letta Code remote environment through Letta’s hosted router. It carries the same runtime protocol as [Letta App Server](/platform/app-server/index.md), with hosted environment discovery, authentication, relay channels, and delivery acknowledgements around it.

For most applications, use the [Letta Agent SDK](/agent-sdk/index.md) with `backend: "cloud"` instead. The SDK resolves the environment, opens both hosted relay sockets, starts the runtime, handles acknowledgements and heartbeats, streams events, and synchronizes state after event gaps.

Use the Remote client API directly only when you are building a custom client, router, or SDK-level integration that must own the hosted WebSocket transport.

A directly connected App Server uses one bidirectional WebSocket. The Agent SDK currently opens two hosted relay sockets labeled `control` and `stream`. Those labels are a client-side convention: both sockets subscribe to the same event feed and the endpoint accepts commands from either one.

## How it fits together

| Piece                                             | Meaning                                                                 |
| ------------------------------------------------- | ----------------------------------------------------------------------- |
| [Device (Computer)](/platform/computers/index.md) | The machine, VM, container, or sandbox where Letta Code executes tools. |
| Connection                                        | The device’s current hosted relay lease, identified by `connectionId`.  |
| Runtime                                           | The `{ agent_id, conversation_id }` pair being executed on that device. |
| Client                                            | Your UI, service, or router that sends commands and renders events.     |

A device has a stable `deviceId`. Its `connectionId` is usually reused across transient reconnects, but may rotate after the device re-registers. Resolve the current connection before opening hosted WebSockets instead of persisting it indefinitely.

## Hosted flow

### 1. Find an online environment

Terminal window

```
curl -sS 'https://api.letta.com/v1/environments?onlineOnly=true' \
  -H "Authorization: Bearer $LETTA_API_KEY"
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
      "currentMode": "standard"
    }
  ],
  "hasNextPage": false
}
```

Choose an online environment whose `connectionId` is non-null.

### 2. Open both relay channels

Open two WebSockets with the same runtime query parameters:

```
wss://api.letta.com/v1/environments/{connectionId}/status/ws?agentId={agentId}&conversationId={conversationId}&channel=control
wss://api.letta.com/v1/environments/{connectionId}/status/ws?agentId={agentId}&conversationId={conversationId}&channel=stream
```

By convention, send commands on the control socket. Read and acknowledge frames from both sockets. Because both subscribe to the same feed, responses and events can be duplicated across them. Correlate direct responses by `request_id`, ignore responses for requests already resolved, and deduplicate events carrying an `idempotency_key`.

Authenticate with `Authorization: Bearer <token>` when your WebSocket implementation supports headers. Browser clients can instead use the `token` query parameter over `wss://`.

### 3. Start the runtime

After both sockets open, send `runtime_start` on the control socket and wait for the matching `runtime_start_response`:

```
{
  "type": "runtime_start",
  "request_id": "runtime-1",
  "agent_id": "agent-...",
  "conversation_id": "conv-...",
  "recover_approvals": false,
  "force_device_status": true,
  "client_info": {
    "name": "my_client",
    "title": "My client"
  }
}
```

Use the `runtime` returned by the response for later scoped commands.

### 4. Send a turn

```
{
  "type": "input",
  "runtime": {
    "agent_id": "agent-...",
    "conversation_id": "conv-..."
  },
  "payload": {
    "kind": "create_message",
    "messages": [
      {
        "role": "user",
        "content": "What files should I inspect first?",
        "client_message_id": "cm_01J_demo"
      }
    ]
  }
}
```

Read `stream_delta` for output and `update_loop_status` for runtime state. A `stream_delta` whose `delta.message_type` is `stop_reason` normally marks turn completion.

### 5. Maintain and recover the connection

- Send `ping` on both sockets periodically; the hosted transport replies with `pong`.
- ACK each frame containing `seq` on the same socket that delivered it.
- Deduplicate replayed events by `idempotency_key`, and direct responses by `request_id`.
- If `event_seq` skips a value, send `sync` on the control socket.
- After transport loss, create a fresh connection or Agent SDK session. `runtime_start` performs the initial state replay; request approval recovery explicitly when needed.

## Minimal client

This Node example shows the transport shape. Production clients should also add timeouts, reconnect backoff, event-gap recovery, and explicit error handling.

```
import WebSocket from "ws";


const token = process.env.LETTA_API_KEY!;
const connectionId = "conn-...";
const runtime = {
  agent_id: "agent-...",
  conversation_id: "conv-...",
};


function open(channel: "control" | "stream") {
  const url = new URL(
    `wss://api.letta.com/v1/environments/${connectionId}/status/ws`,
  );
  url.searchParams.set("agentId", runtime.agent_id);
  url.searchParams.set("conversationId", runtime.conversation_id);
  url.searchParams.set("channel", channel);


  return new WebSocket(url, {
    headers: { Authorization: `Bearer ${token}` },
  });
}


const control = open("control");
const stream = open("stream");
const resolvedRequestIds = new Set<string>();
const seenEventIds = new Set<string>();


function send(frame: unknown) {
  control.send(JSON.stringify(frame));
}


for (const socket of [control, stream]) {
  socket.on("message", (raw) => {
    const frame = JSON.parse(raw.toString());


    if (typeof frame.seq === "number") {
      socket.send(JSON.stringify({ type: "ack", seq: frame.seq }));
    }
    if (
      typeof frame.request_id === "string" &&
      resolvedRequestIds.has(frame.request_id)
    ) {
      return;
    }
    if (frame.type.endsWith("_response") && frame.request_id) {
      resolvedRequestIds.add(frame.request_id);
      handleResponse(frame);
    }
    if (
      typeof frame.idempotency_key === "string" &&
      seenEventIds.has(frame.idempotency_key)
    ) {
      return;
    }
    if (typeof frame.idempotency_key === "string") {
      seenEventIds.add(frame.idempotency_key);
    }
    if (frame.type === "stream_delta") renderDelta(frame.delta);
    if (frame.type === "update_loop_status") renderStatus(frame.loop_status);
  });
}


await Promise.all(
  [control, stream].map(
    (socket) => new Promise<void>((resolve) => socket.once("open", resolve)),
  ),
);


send({
  type: "runtime_start",
  request_id: "runtime-1",
  agent_id: runtime.agent_id,
  conversation_id: runtime.conversation_id,
  recover_approvals: false,
  force_device_status: true,
});


setInterval(() => {
  for (const socket of [control, stream]) {
    if (socket.readyState === WebSocket.OPEN) {
      socket.send(JSON.stringify({ type: "ping" }));
    }
  }
}, 30_000);


// In a real client, wait for runtime_start_response before sending input.
```

## Protocol references

- [Remote client API reference](/agent-sdk/remote-client/reference/index.md) - Hosted discovery, auth, relay channels, startup, and reliability.
- [App Server protocol lifecycle](/platform/app-server/protocol-lifecycle/index.md) - Canonical commands, responses, approvals, and runtime events.
- [Self-hosting](/self-hosting/index.md) - Run local agents on infrastructure you control and connect through App Server.
