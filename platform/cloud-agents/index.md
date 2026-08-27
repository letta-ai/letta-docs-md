---
title: Cloud agents | Letta Docs
description: Run your stateful agents in cloud computers
---

Any Letta agent can be run on [chat.letta.com](https://chat.letta.com/) as a cloud agent, executing in a cloud sandbox instead of on your own computer.

The benefits of running agents in the cloud are:

- **Always available & long-running**: Agents can still be messaged even if your laptop is closed, since they have their own computer to run on. Combining agents with [Slack](/platform/cloud-agents/slack/index.md) and [schedules](/configuration/schedules/index.md) allows you to create always-on digital coworkers.
- **Concurrent work at scale**: Run hundreds or even thousands of parallel conversations, each in its own isolated computer.
- **Security & isolation**: Agents can only access the secrets and resources you’ve configured for their cloud computer.

Since Letta agents are stateful, they still have the same memory even when working in the cloud and can access session history from any machine.

## Running cloud agents

If you’re using the [desktop app](/platform/desktop-app/index.md), your agent will execute on your local computer by default — for example, allowing it to access local files or programs installed on your local machine. You can replace the “Local” selection with “Cloud” in the dropdown under your chat window to move your agent to the cloud.

If you log into our web app at [chat.letta.com](https://chat.letta.com), your agent will execute on a **cloud computer** (or “cloud sandbox”) by default. Agents can also run on other registered computers.

You can always change the computer an agent is running from (e.g. “teleporting” from local to cloud). Agents will not lose their session history or memory when moving across computers.

## Configuring cloud agents

We recommend configuring cloud agents with [secrets](/configuration/secrets/index.md) so they can still access resources from the cloud sandbox, and also adding the [GitHub](/platform/cloud-agents/github/index.md) and [Slack](/platform/cloud-agents/slack/index.md) integrations.

## Cloud agents with the Agent SDK

You can also run cloud agents programmatically with the [Agent SDK](/agent-sdk/index.md). Use `backend: "cloud"` and don’t specify a `computer` — the SDK automatically creates a managed cloud sandbox for each session. The sandbox is where the agent’s tools run, while its memory and conversation state remain hosted in Letta Cloud.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


const agentId = await client.createAgent({
  persona: "You are a research assistant that can browse, write code, and remember durable context.",
});


await using session = client.resumeSession(agentId);
```

To run the agent on a specific machine instead of a sandbox, pass a `computer` selector (for example, `computer: { name: "work-laptop" }`) — `computer` and sandbox mode are mutually exclusive. For sandbox lifecycle options and computer selection details, see [Deploying your agents](/agent-sdk/deployment/index.md).

## Bring your own computers

To make a computer available from [chat.letta.com](https://chat.letta.com), install the Letta CLI on that computer, then run `letta server` to connect it to your Letta account. You can also install the desktop app and select “Allow remote access”. For more information, see [Bring your own machine](/platform/computers/byom/index.md).
