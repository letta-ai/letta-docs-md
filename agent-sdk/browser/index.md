---
title: Browser and React Native | Letta Docs
description: Use the Agent SDK in browser, Expo, and React Native applications
---

Browser, Expo, and React Native applications must import the SDK from `@letta-ai/letta-agent-sdk/client`:

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk/client";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: userProvidedApiKey,
  webSocketAuth: "query",
});
```

This import supports `backend: "cloud"` and `backend: "remote"`. It does not support the local backend or MCP servers. Both require Node.js.

## Available features by import

| Capability                           | Browser and React Native import | Node.js import                                     |
| ------------------------------------ | ------------------------------- | -------------------------------------------------- |
| `backend: "cloud"`                   | ✅                               | ✅                                                  |
| `backend: "remote"`                  | ✅                               | ✅                                                  |
| `backend: "local"`                   | ❌                               | ✅                                                  |
| MCP servers (`mcpServers`)           | ❌                               | ✅                                                  |
| Client tools (`tools`)               | ✅                               | ✅                                                  |
| Repositories (`client.repositories`) | ✅                               | ✅                                                  |
| Image helper functions               | None                            | `imageFromFile`, `imageFromBase64`, `imageFromURL` |

In Node.js, import from `@letta-ai/letta-agent-sdk` to use the local backend or MCP servers. The local backend starts an App Server process. The SDK starts stdio MCP servers and connects to HTTP or SSE MCP servers from your Node.js application.

## Browser authentication

Browser WebSockets cannot set upgrade headers, so cloud clients in the browser should use `webSocketAuth: "query"` to send credentials in the connection URL instead:

```
const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: userProvidedApiKey,
  webSocketAuth: "query",
});
```

An API key shipped to the browser is visible to the user. Issue short-lived, user-scoped credentials from your backend rather than embedding an organization-wide key in client code.

## React Native

For an authenticated remote App Server in React Native, adapt the platform WebSocket constructor so the SDK can pass the `Authorization` header:

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

## Send messages from a browser or React Native application

Sessions work the same as in Node: create or resume a session, send, and stream. See [Sending messages](/agent-sdk/messages/index.md) for the full event-handling patterns.

`extractStreamTextDelta()` returns the next text fragment and labels it as `assistant` or `reasoning`. It returns `null` when the event contains no text.

```
import { extractStreamTextDelta } from "@letta-ai/letta-agent-sdk/client";


await using session = client.resumeSession(agentId);


await session.send("Summarize my unread updates.");


let response = "";
for await (const message of session.stream()) {
  if (message.type !== "stream_event") continue;


  const delta = extractStreamTextDelta(message.event);
  if (delta?.kind === "assistant") response += delta.text;
}


console.log(response);
```

This example collects assistant text only. Handle `reasoning` fragments separately if your application displays them.

The browser and React Native import does not include image helper functions. To send an image, create an `ImageContent` value from base64 data:

```
import type { ImageContent } from "@letta-ai/letta-agent-sdk/client";


const image = {
  type: "image",
  source: {
    type: "base64",
    media_type: "image/png",
    data: uploadedBase64,
  },
} satisfies ImageContent;


await session.send([{ type: "text", text: "Describe this image." }, image]);
```

Set `data` to the raw base64 string. Do not include a `data:` URL prefix. In Node.js, import the image helper functions from `@letta-ai/letta-agent-sdk`.

## What to read next

- [Sending messages](/agent-sdk/messages/index.md) — the full event-handling patterns
- [Examples](/agent-sdk/examples/index.md) — including the web-chat example app
- [Deployment](/agent-sdk/deployment/index.md) — choosing cloud vs remote backends
