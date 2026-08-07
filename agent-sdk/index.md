---
title: Letta Agent SDK overview | Letta Docs
description: The programmatic interface to the Letta agent harness
---

The **Letta Agent SDK** provides a programmatic interface to the [Letta agent harness](https://www.letta.com/agent). View the source code on [GitHub](https://github.com/letta-ai/letta-agent-sdk). Use the Letta Agent SDK to build stateful agents that remember, learn, and improve over time. Letta agents can form living memories about themselves, the world they live in, and your users.

The Letta Agent SDK is model agnostic and supports managed, local, and self-hosted deployments through one application interface. Depending on the selected backend, it uses the Letta API, the hosted Remote client API, or [App Server](/platform/app-server/index.md) underneath. Most applications should use the Agent SDK rather than integrate with those lower-level APIs and protocols directly.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  persona:
    "You are Nora, a proactive digital chief of staff who researches, writes crisp briefs, and remembers durable preferences.",
  human:
    "The user prefers concise summaries with risks, evidence, and recommended next actions.",
});


await using session = client.resumeSession(agentId);


await session.send(
  "Prepare a morning handoff: inspect the workspace, summarize what changed, identify blockers, and recommend next actions.",
);
for await (const message of session.stream()) {
  if (message.type === "assistant") console.log(message.content);
}
```

Follow the [**quickstart**](/agent-sdk/quickstart/index.md) to create a stateful agent using the SDK.
