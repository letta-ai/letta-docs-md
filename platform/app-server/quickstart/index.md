---
title: Quickstart | Letta Docs
description: Start the Letta App Server, connect over WebSocket, and submit input
---

The recommended way to interface with the App Server is the [Letta Agent SDK](/agent-sdk/index.md), which provides a high-level interface over its WebSocket protocol.

Alternatively, use the App Server’s [OpenAI-compatible API](/platform/app-server/quickstart#openai-compatible-api/index.md) with clients such as Open WebUI, or the [ACP adapter](/platform/acp/index.md) with ACP clients such as Zed.

For most application integrations, start with the [Letta Agent SDK quickstart](/agent-sdk/quickstart/index.md). The SDK manages App Server and provides high-level APIs for agents, sessions, turns, streaming, and approvals.

Continue with this guide when you need to operate App Server separately or connect to its protocol directly. The examples use the local backend so agent state and the execution environment remain on the App Server machine.

## Install the Letta CLI

Terminal window

```
npm install -g @letta-ai/letta-code
```

## Start the server

Run App Server on a fixed local port during development:

Terminal window

```
letta server --backend local --listen ws://127.0.0.1:4500
```

The process prints the base URL and its WebSocket endpoint:

```
Listening on ws://127.0.0.1:4500
WebSocket: ws://127.0.0.1:4500/ws
```

App Server uses one bidirectional WebSocket. Legacy `?channel=control` and `?channel=stream` URLs are rejected with HTTP 426.

To bind to an available loopback port, omit the URL:

Terminal window

```
letta server --backend local --listen
```

App Server prints the selected URL at startup.

`letta app-server` remains available as a deprecated compatibility alias. New integrations should use `letta server --listen`.

For a non-loopback listener, configure websocket auth. For example, capability-token auth reads a token from an absolute path and requires clients to send it as a bearer token:

Terminal window

```
letta server \
  --backend local \
  --listen ws://0.0.0.0:4500 \
  --ws-auth capability-token \
  --ws-token-file /absolute/path/to/app-server-token
```

You can also use signed bearer tokens with `--ws-auth signed-bearer-token` and `--ws-shared-secret-file /absolute/path/to/secret`.

## OpenAI-compatible API

Add `--openai-api` to any `letta server --listen` command to use OpenAI-compatible clients such as Open WebUI, LibreChat, LobeChat, or the OpenAI SDKs:

Terminal window

```
letta server --backend local --listen ws://127.0.0.1:4500 --openai-api
```

Set the client’s base URL to `http://127.0.0.1:4500/v1`. App Server exposes:

- **`GET /v1/models`**: Lists each Letta agent as a model.
- **`POST /v1/chat/completions`**: Sends Chat Completions requests to the selected agent, with streaming and image inputs supported.
- **`POST /v1/responses`**: Sends Responses API requests with streaming, text and image inputs, instructions, and server-executed tool activity represented as `function_call` and `function_call_output` items.

Use the official OpenAI SDK by selecting an agent from `/v1/models`:

Call the Responses API

```
import OpenAI from "openai";


const client = new OpenAI({
  apiKey: "local-app-server",
  baseURL: "http://127.0.0.1:4500/v1",
});


const models = await client.models.list();
const model = models.data[0]?.id;
if (!model) throw new Error("Create a Letta agent before sending a response");


const response = await client.responses.create({
  model,
  input: "Inspect this repository and summarize its architecture.",
});


console.log(response.output_text);
```

Responses start in a fresh temporary Letta conversation unless the client sends a stable `X-Letta-Chat-Key` header. Stored responses and `previous_response_id` are not supported; send the input history again or use that header for conversation continuity.

When App Server authentication is configured, pass the same bearer token as the client’s API key.

## Connect with the client helper

Use the exported App Server client for TypeScript integrations.

Terminal window

```
npm install @letta-ai/letta-code ws
```

app-server-client.ts

```
import WebSocket from "ws";
import { createAppServerClient } from "@letta-ai/letta-code/app-server-client";


const client = await createAppServerClient({
  url: "ws://127.0.0.1:4500",
  WebSocket,
}).connect();


const info = await client.info();
console.log(info.protocol_version, info.capabilities);


client.onMessage((message) => {
  console.log(message.type);
});
```

The client opens one `/ws` connection. `client.info()` reports the server version, protocol version, backend, and capabilities; check these before relying on optional commands.

If the server uses capability-token auth, pass the token to the helper when your WebSocket implementation supports headers:

```
const authToken = process.env.APP_SERVER_TOKEN;
if (!authToken) throw new Error("APP_SERVER_TOKEN is required");


const client = await createAppServerClient({
  url: "ws://example.internal:4500",
  authToken,
  WebSocket,
}).connect();
```

## Start a runtime

Start a runtime for an existing agent and conversation:

```
const started = await client.runtimeStart({
  agent_id: "agent-123",
  conversation_id: "conv-123",
  cwd: "/Users/me/project",
  mode: "standard",
  client_info: {
    name: "my_app",
    title: "My App",
    version: "0.1.0",
  },
});


if (!started.success || !started.runtime) {
  throw new Error(started.error ?? "Failed to start runtime");
}


const runtime = started.runtime;
```

Create a new conversation for an existing agent by omitting `conversation_id` and passing `create_conversation`:

```
const started = await client.runtimeStart({
  agent_id: "agent-123",
  create_conversation: {
    body: {},
  },
  cwd: "/Users/me/project",
});
```

Create a new agent and conversation in one call:

```
const started = await client.runtimeStart({
  create_agent: {
    body: {
      name: "App Server Agent",
      memory_blocks: [],
    },
  },
  create_conversation: {
    body: {},
  },
  cwd: "/Users/me/project",
  mode: "acceptEdits",
});
```

`runtime_start_response.runtime` is the canonical scope for future commands. Store and reuse it.

## Observe stream events

The main streamed output is `stream_delta`:

```
client.onMessage((message) => {
  if (message.type !== "stream_delta") return;
  if (
    message.runtime.agent_id !== runtime.agent_id ||
    message.runtime.conversation_id !== runtime.conversation_id
  )
    return;


  const delta = message.delta;
  if ("message_type" in delta && delta.message_type === "loop_error") {
    console.error(delta.message);
    return;
  }


  console.log(delta);
});
```

`stream_delta.delta` can be either a standard Letta streaming message delta or an App Server lifecycle event such as tool starts/ends, command output, retries, status messages, and terminal stop reasons. Handle unknown delta shapes defensively and preserve them in logs while the protocol evolves.

## Send input

App Server execution is event-driven. Register protocol event handlers before calling `input()` so the controller observes the complete turn lifecycle. `input()` returns after writing the command to the WebSocket; output, tool activity, approvals, status changes, and terminal events arrive through the same connection.

```
client.input({
  runtime,
  payload: {
    kind: "create_message",
    messages: [
      {
        role: "user",
        content: "Run the relevant tests.",
        client_message_id: "request-123",
      },
    ],
  },
});
```

Reuse the same `client_message_id` when retrying delivery of one logical user message.

## Sync state

Call `sync` when a connected UI needs a fresh snapshot:

```
await client.sync({
  runtime,
  recover_approvals: false,
  force_device_status: true,
});
```

`recover_approvals: false` is useful for lightweight UI refreshes. Leave it unset when you want App Server to probe backend state for stale pending approvals. After transport loss, open a fresh client and call `runtimeStart` again to restore the runtime subscription and any connection-owned external tools; `runtimeStart` performs an initial state replay.

## Abort active work

Cancel an active turn with `abort_message`:

```
const aborted = await client.abort({ runtime });
console.log(aborted.aborted);
```

## Minimal raw websocket flow

If you do not use the helper, send native JSON frames over the WebSocket and receive all responses and events on that same connection.

runtime\_start

```
{
  "type": "runtime_start",
  "request_id": "runtime-1",
  "agent_id": "agent-123",
  "conversation_id": "conv-123",
  "cwd": "/Users/me/project",
  "mode": "standard"
}
```

input

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
        "content": "Summarize this project."
      }
    ]
  }
}
```

## Next steps

- [Protocol lifecycle](/platform/app-server/protocol-lifecycle/index.md) - Learn the command and event flow.
- [External tools](/platform/app-server/external-tools/index.md) - Register tools that execute in your controller.
- [Integration patterns](/platform/app-server/integration-patterns/index.md) - Design robust controllers and team orchestrators.
