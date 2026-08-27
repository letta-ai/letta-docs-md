---
title: Build a mobile agent app | Letta Docs
description: Run a complete Expo mobile client for Letta Cloud or your own App Server
---

The [Agent SDK mobile app](https://github.com/letta-ai/agent-sdk-mobile-app) is a complete Expo and React Native client for persistent Letta agents. It can connect to Letta Cloud or directly to a Letta App Server running on your own computer.

Use this demo when you want to study a mobile interface with conversation history, streaming, tools, approvals, interruption, queued messages, image attachments, and reconnect handling already wired to the portable Agent SDK.

## Run the app

Clone the repository and start the iOS or Android build:

```
git clone https://github.com/letta-ai/agent-sdk-mobile-app.git
cd agent-sdk-mobile-app
bun install
bun run ios
# or: bun run android
```

You can also use `npm install` and the equivalent npm scripts.

The first screen offers two connection choices:

- **Letta Cloud** opens the browser for OAuth or accepts a Letta API key. The app stores credentials in the device keychain with `expo-secure-store`.
- **Your own server** connects to a Letta App Server over WebSocket. Start one on the computer where you want the agent to run tools:

```
npm install -g @letta-ai/letta-code
openssl rand -hex 24 > /tmp/ws-token
letta server --listen ws://0.0.0.0:4610 \
  --ws-auth capability-token \
  --ws-token-file /tmp/ws-token
```

Enter `ws://<your-machine>:4610` and the generated token in the app. Use TLS or a private network when the server is available beyond your local network. An agent connected to this server can read files and run commands on that computer.

## What it demonstrates

- Browsing and managing agents and conversations through the portable client
- Streaming assistant text, reasoning, tool calls, and tool results
- Reducing live events and saved history with `createTranscriptAccumulator()`
- Showing tool approval requests and changing permission modes
- Interrupting a turn and queuing follow-up messages
- Sending screenshots and photos as image input
- Reconnecting after the app moves between foreground and background
- Keeping Cloud credentials in the device keychain

## Follow the SDK integration

The main SDK path is intentionally small:

| File                                    | What it shows                                                                          |
| --------------------------------------- | -------------------------------------------------------------------------------------- |
| `src/lib/letta/ChatSession.ts`          | Resume a session, consume `stream()`, resolve approvals, interrupt, and queue messages |
| `src/lib/letta/transcriptProjection.ts` | Project SDK transcript rows into mobile render state                                   |
| `src/lib/letta/api.ts`                  | Manage agents, conversations, models, and message history through the portable client  |
| `src/lib/letta/model.ts`                | Define the state shared by the real and mock transports                                |
| `src/lib/letta/mockSession.ts`          | Render every UI state without credentials or a running server                          |

The app imports `@letta-ai/letta-agent-sdk/client`, so its UI code works in React Native without Node.js runtime dependencies. Run the `/gallery` route to inspect all component states against the mock transport.

For the full screen map and connection lifecycle, read the repository’s [`docs/design-doc.md`](https://github.com/letta-ai/agent-sdk-mobile-app/blob/main/docs/design-doc.md) and [`docs/architecture.md`](https://github.com/letta-ai/agent-sdk-mobile-app/blob/main/docs/architecture.md).
