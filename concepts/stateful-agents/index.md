---
title: Stateful agents | Letta Docs
description: Understand how a Letta agent preserves identity and state over time
---

A **stateful agent** is a persistent AI identity with its own memory, model configuration, tools, and message history. You can return to the same agent across sessions, computers, and interfaces instead of starting from scratch each time.

## What belongs to an agent

Each agent has:

- A name and description
- A personality and system prompt
- Long-term memory stored in [MemFS](/concepts/memfs/index.md)
- Model and tool configuration
- One or more [conversations](/concepts/conversations/index.md)

Memory is shared across an agent’s conversations. A preference learned in one conversation can therefore improve how the agent works in another.

## Switching agents

Use `/agents` in the CLI to browse and switch agents. Pin an agent with `/pin` or the favorite control in the desktop app so it is easier to find later.

```
> /agents
> /pin
```

Use separate agents when you want independent identities or memory. Use separate conversations when you want parallel threads with the same identity and memory.

## Where agents are stored

When you sign in with Letta, your agents are backed up to the cloud and available through the desktop app, CLI, and web app. You can run the same agent on any connected [computer](/platform/computers/index.md).

Agents created without a Letta account are stored only on local disk. They cannot be accessed remotely through the web app and may require manual backups. See [Local setup](/self-hosting/index.md).
