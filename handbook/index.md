---
title: The Letta Handbook | Letta Docs
description: A practical guide to building agents that learn, adapt, and run on their own.
---

The Letta Handbook is an opinionated guide to building agents that learn over time. For detailed configuration and reference material, use the [Letta app and CLI documentation](/index.md).

Most AI tools preserve chat history, but chat history is not the same as durable memory. A Letta agent can maintain and edit useful information about you, its work, and its environment across conversations.

Working with a Letta agent is closer to collaborating with a long-term colleague than repeatedly starting from a blank chat.

This handbook gets you started quickly with your first agent, but it also contains practices that experienced agent builders can use.

Letta agents are most commonly used as coding agents that learn projects in detail. They are also used as personal assistants, knowledge managers, operations agents, and companions.

## How this handbook is organized

The handbook follows the arc of working with one agent over time. You can apply the same principles when working with multiple agents.

1. **[Set up Letta](/handbook/setup/index.md)**: Install the Letta app, connect a model provider, and prepare your workspace.
2. **[Meet your agent](/handbook/meet-your-agent/index.md)**: Create your first agent, introduce yourself, and confirm that memory persists.

More chapters are coming soon.

## What people build

One agent can serve several of these roles and switch between them as needed.

**Coding partners** learn your repositories, style guides, and habits as you work together. They can review pull requests, run test suites, debug failures, and maintain documentation. Some people use one persistent agent that accumulates project knowledge over time, while others delegate focused tasks to stateless subagents.

**Operations agents** handle scheduled work such as planning, triage, and reporting. People build daily briefing agents, email triage assistants, and task managers that track open loops. These agents rely on schedules and messaging integrations to show up with the right information at the right time.

**Research and knowledge agents** organize and retrieve information without cluttering your active conversation. They can manage literature reviews, curate reference libraries, and synthesize findings across long projects. Structured reference files and search keep detailed material available without loading it on every turn.

**Companions and creative partners** maintain persistent personalities and histories. People build long-running companion agents, roleplay characters, and collaborative fiction writers. These agents can be reached through the desktop app, CLI, or supported [Channels](/configuration/channels/index.md) such as Telegram and Discord.

## Why Letta?

If you are tired of explaining the same context to an AI over and over, Letta is built to solve that.

- **Living memory**: Your agent edits its own memory based on your feedback. Reflection workflows can review recent conversations, consolidate what the agent learned, and write useful lessons into memory. Agent memory is represented as git-backed files that you can inspect, edit, and version.
- **Model flexibility**: Your agent’s saved memory is not tied to one model provider. You can switch among supported models without recreating the agent, although different models may behave differently.
- **Skills that grow**: Your agent can learn repeatable workflows as skills and improve those skills over time.
- **Proactive agency**: With schedules, Channels, and a runtime that stays online, an agent can perform recurring work and report back when something needs attention.
- **Available across environments**: Sign in with Letta to carry the same agent memory and conversations across the desktop app, CLI, web chat, remote machines, and supported messaging integrations.
- **Local when you want it**: The Letta app and CLI can run agents without a Letta account using local state, connected model providers, or local inference. Agent memory remains directly inspectable on your machine.

## Next step

[Set up Letta](/handbook/setup/index.md) and create your first persistent agent.
