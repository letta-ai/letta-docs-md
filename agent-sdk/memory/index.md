---
title: Memory | Letta Docs
description: How a Letta agent remembers — setting memory, what stays in context, and dreaming
---

Memory is what makes a Letta agent stateful. An agent’s memory is its own: it persists across conversations, follows the agent between models and computers, and the agent edits it as it learns.

## Persona and human shorthand

`persona` and `human` are conveniences that set the agent’s persona and human memory:

```
const agentId = await client.createAgent({
  persona: "You are a resident engineering teammate for this repository.",
  human: "The user prefers practical handoffs with commands to run.",
});
```

## Setting memory at creation

Pass `memory` for full control over the agent’s starting memory. Each entry becomes a Markdown file in the agent’s memory repository, named from its label:

```
const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  memory: [
    {
      label: "persona",
      value: "You are Quinn, a digital research analyst.",
    },
    {
      label: "team-context",
      value: "The team ships weekly on Thursdays. Staging is at stage.example.com.",
    },
  ],
});
```

Use objects with `label` and `value`; creation backends reject memory preset names.

[Shared memory repositories](/agent-sdk/repositories/index.md) give several agents access to the same files. Attaching one recompiles the agent’s system prompt so the repository shows up in its context — as a file tree it reads from on demand, rather than inlined the way `system/` memory is. Repositories are hosted by Letta, so they are a cloud feature; self-hosted deployments can share memory by pointing agents at their own git remote.

## MemFS

An agent’s memory is part of its state, not a folder on a machine: it lives in a git repository owned by the agent, which MemFS **projects** onto whatever computer the agent is working on. Edits become memory once they are committed and pushed. See [MemFS](/concepts/memfs/index.md) for the full model.

Two things matter when you are writing against the SDK:

- A memory entry’s label becomes its path in the repository, and memory you set at creation lands under `system/`.
- Files under `system/` are in the system prompt every turn. Everything else stays out of context — the agent sees the file tree and reads what it needs.

To find the memory directory on the computer the agent is working on, ask the session:

```
const { memoryDirectory } = await session.getDeviceStatus();
// → "/root/.letta/agents/agent-3f97f111-…/memory"
```

## Dreaming

[Dreaming](/configuration/memory/index.md) uses background subagents to review recent conversations, consolidate lessons, and update memory without interrupting active work. Configure it with `dreaming`:

```
const agentId = await client.createAgent({
  persona: "You are a support engineer who learns each customer's environment.",
  dreaming: {
    trigger: "step-count", // "off" | "step-count" | "compaction-event"
    behavior: "auto-launch", // "reminder" | "auto-launch"
    stepCount: 25,
  },
});
```

- `trigger` controls when dreaming runs: after a number of steps, on context compaction, or never.
- `behavior` controls what happens at the trigger: remind the agent to update memory, or automatically launch a background dreaming subagent. It can only be set at agent creation.
- `stepCount` is the step interval for the `"step-count"` trigger.

Sessions can override `trigger` and `stepCount` (but not `behavior`) with the session `dreaming` option. The `init` message reports the effective settings for a session.

## What to read next

- [Creating agents](/agent-sdk/agents/index.md) — setting memory and dreaming at creation time
- [Shared memory](/agent-sdk/repositories/index.md) — versioned repositories shared between agents
- [MemFS](/concepts/memfs/index.md) — the git-backed memory filesystem in depth
