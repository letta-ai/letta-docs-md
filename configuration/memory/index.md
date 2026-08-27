---
title: Memory & dreaming | Letta Docs
description: Initialize, teach, and improve your agent's memory over time
---

Letta agents use [MemFS](/concepts/memfs/index.md), a git-backed memory filesystem that they can inspect and edit. Memory is shared across the agent’s conversations and improves as the agent learns durable information about you and its work.

## Initialize memory

Run `/init` to bootstrap or refresh memory for the current project. The agent inspects the repository, asks about your working style when needed, and can review prior coding sessions using [subagents](/configuration/subagents/index.md).

```
> /init
```

If the memory hierarchy has drifted or grown too large, run `/doctor` to audit placement, duplication, and system-prompt token usage.

## Teach your agent

Your agent updates memory when it learns something durable. You can also teach it explicitly with `/remember`:

```
> /remember always use pnpm in this repo
```

The agent decides where the lesson belongs and commits the update to MemFS. Use the memory viewer in the desktop app or inspect `$MEMORY_DIR` directly to review what it saved.

## Dreaming

Dreaming uses background subagents to review recent conversations, consolidate useful lessons, and update memory without interrupting your active work.

Configure dreaming with `/sleeptime` in the CLI or **Dream settings** in the app. Choose when it runs: after a set number of completed agent steps or when the context window is compacted.

Select **Agent reviews before applying** to have your agent review and revise proposed memory updates in a second background conversation. This uses more model tokens and does not ask you for approval.

## Reorganize memory

For larger cleanups, ask the agent to reorganize its memory. The memory workflow backs up the current repository before splitting large files, merging duplicates, or restructuring the hierarchy.

See [MemFS](/concepts/memfs/index.md) for the directory structure, versioning model, synchronization behavior, and agent-owned skills.
