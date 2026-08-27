---
title: Add agents to an existing desktop app | Letta Docs
description: Study a Letta Agent SDK integration inside the Signal Desktop application shell
---

The [Signal Desktop shell demo](https://github.com/letta-ai/signal-desktop-app) shows how to connect the Letta Agent SDK to a large existing desktop application. It keeps Signal Desktop’s contact list, conversations, composer, local message history, attachments, typing indicators, failed-send state, and retry interface while replacing the messaging backend with Letta agents and conversations.

This repository is an integration demo. It is not a Signal client for the Signal network, an official Signal release, or a starter architecture for a new chat application. Use the [React chat demo](/agent-sdk/demo-apps/react-chat/index.md) when you want a small frontend to customize. Use this demo when you want to see the SDK adapted to an existing application’s data model and UI lifecycle.

## Run the demo

Signal Desktop currently requires Node.js 24.17.0 and pnpm 11.5.2:

```
git clone https://github.com/letta-ai/signal-desktop-app.git
cd signal-desktop-app
nvm install
nvm use
pnpm install
pnpm generate
LETTA_API_KEY=sk-let-... pnpm start
```

Set `LETTA_MODE=0` to run the upstream Signal behavior instead of the Agent SDK integration. You can also set `LETTA_RUNTIME_API_KEY` when agent turns should use a different credential from agent discovery.

## What it demonstrates

- Representing Letta agents as contacts in an existing application
- Giving each contact a dedicated persistent Letta conversation
- Connecting the existing send action to `session.send()`
- Folding `session.stream()` through `createTranscriptAccumulator()`
- Projecting assistant rows into the host application’s native message records
- Reusing optimistic sends, local history, typing state, failure state, and retry
- Sending supported image attachments as Agent SDK multimodal content
- Transcribing voice memos before sending their text to an agent
- Loading agent profile pictures from MemFS into the existing avatar system

## Follow one message

The integration lives primarily in `ts/services/letta.preload.ts`:

1. Signal creates and stores an outgoing message through its normal composer and message model.
2. On the first send to a contact, the adapter creates a Letta conversation and resumes it through the portable Agent SDK client.
3. The adapter passes the message and supported image attachments to `session.send()`.
4. Stream messages pass through the SDK transcript accumulator.
5. Assistant rows become incoming Signal messages and update as text arrives.
6. SDK or transcription failures use Signal’s existing failed-send state and **Retry Send** action.

Agent and conversation management use the SDK’s `agents` and `conversations` namespaces. The profile-picture endpoint remains direct API code because the portable SDK does not expose it.

## Demo boundaries

- Reasoning, tool-call, and tool-result rows are not rendered.
- The demo has no approval interface. Sessions use unrestricted permissions and an allow-all `canUseTool` callback, so available tools can run without asking in the UI.
- Image input is limited to PNG, JPEG, GIF, and WebP.
- The first remote-history import is limited to 100 messages.
- Voice memo audio goes to the transcription provider selected in the app. Only the returned text is sent to the Letta agent.

Read the repository’s [`LETTA_FORK.md`](https://github.com/letta-ai/signal-desktop-app/blob/main/LETTA_FORK.md) for the complete list of integration points and scope limits.
