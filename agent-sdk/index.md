---
title: Letta Agent SDK overview | Letta Docs
description: The SDK for stateful agents — create an agent once, then resume it from anywhere
---

The **Letta Agent SDK** is the SDK for [stateful agents](/concepts/stateful-agents/index.md): create an agent once, then resume it from anywhere. Each agent has its own identity and long-term memory, and keeps both across conversations, models, and the computers it runs on.

That makes the agent — not the process, the session, or the machine — the durable object in your application. Most of the time you are reconnecting to an agent that already exists and already knows something, rather than creating a disposable one. Use the SDK to build multi-agent and multi-user applications, orchestrate agents dynamically, or put a custom interface on top of a Letta agent.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({ backend: "cloud" });


// Create the agent once...
const agentId = await client.createAgent({
  persona: "You are Nora, a research analyst who tracks our competitors.",
});


// ...then resume it, from anywhere, for as long as it lives.
await using session = client.resumeSession(agentId);


await session.send("What changed since last week?");
for await (const message of session.stream()) {
  if (message.type === "assistant") process.stdout.write(message.content);
}
```

## Start in order

1. [**Quickstart**](/agent-sdk/quickstart/index.md): install the SDK, create an agent, and stream its first response
2. [**Sessions, turns, and durability**](/agent-sdk/sessions/index.md): the agent, conversation, and session model that the rest of these docs assume
3. [**Creating agents**](/agent-sdk/agents/index.md) and [**Sending messages**](/agent-sdk/messages/index.md): configure memory and handle the event stream

## What you need

- A JavaScript or TypeScript project
- A [Letta API key](https://platform.letta.com/api-keys) for the cloud backend; the local backend needs no account
- Node.js 22.19+ only if you run the agent runtime yourself — the local backend, or a self-hosted [App Server](/platform/app-server/index.md)

## Choose your next step

Start with the [Quickstart](/agent-sdk/quickstart/index.md) when you are new to the SDK. Read [Deployment](/agent-sdk/deployment/index.md) when you need to decide where agent state lives and where tools execute — the SDK is model agnostic and reaches managed, local, and self-hosted deployments through one interface. Explore the demo apps for a [React chat frontend](/agent-sdk/demo-apps/react-chat/index.md), a [mobile client](/agent-sdk/demo-apps/mobile/index.md), or an [integration inside an existing desktop application](/agent-sdk/demo-apps/signal-desktop/index.md). Browse [Examples](/agent-sdk/examples/index.md) for smaller applications focused on individual SDK features. The source is on [GitHub](https://github.com/letta-ai/letta-agent-sdk).
