---
title: MemFS | Letta Docs
description: Understand the git-backed memory filesystem used by Letta agents
---

**MemFS** is the git-backed filesystem where a Letta agent stores long-term memory. It stores the agent’s memory in Markdown files so the agent can read, edit, organize, and version what it learns. All Letta agents use MemFS.

MemFS is also called a [context repository](https://www.letta.com/blog/context-repositories).

## Memory structure

Each memory file is Markdown with YAML frontmatter:

```
---
description: "Who I am, what I value, and how I approach working with people."
---


I am a Letta agent. I remember durable preferences and improve with use.
```

Files under `system/` are loaded into the agent’s system prompt on every turn. Use this directory for the agent’s identity, important user preferences, durable project facts, and critical workflow rules.

Files outside `system/` remain discoverable through the memory tree, but their full contents are loaded only when relevant. This keeps the active context lean while preserving deeper reference material.

```
$MEMORY_DIR/
├── system/
│   ├── persona.md
│   └── human.md
├── reference/
│   └── project-notes.md
└── skills/
    └── my-skill/
        └── SKILL.md
```

## Semantic and vector search

MemFS does not include a semantic or vector index by default. Agents find memory in its Markdown files with normal file-search and read tools.

For keyword search and optional semantic or hybrid search, install the [MemFS Search mod](https://github.com/letta-ai/mods/tree/main/packages/memfs-search):

```
letta install npm:@letta-ai/memfs-search
```

Keyword search works without additional dependencies. Semantic and hybrid modes require [QMD](https://github.com/tobi/qmd) to be installed and indexed over `$MEMORY_DIR`.

Conversation-history search is separate from MemFS. On Letta Cloud, `letta messages search` supports full-text, vector, and hybrid search over messages; local backends currently search conversation transcripts with full-text matching only.

## Versioning and synchronization

Every memory edit is committed to the MemFS git repository. This provides version history, conflict resolution, and a clear boundary between saved memory and uncommitted changes.

For agents backed up to the cloud, commits sync back to Letta. Local-only agents commit to a repository on the current machine, so you are responsible for backing it up.

Memory subagents such as dreaming and memory doctor use git worktrees so they can update memory concurrently without blocking the main agent.

## Skills in MemFS

Agent-owned skills live under `$MEMORY_DIR/skills`. They are versioned with the rest of the agent’s memory and travel with agents that are backed up to the cloud.

See [Skills](/configuration/skills/index.md) for skill sources, precedence, and authoring.

## Shared memory

Each agent has its own MemFS. Use [shared memory](/concepts/shared-memory/index.md) when multiple cloud-hosted agents need access to the same Git-backed files and working context.

## Managing memory

See [Memory & dreaming](/configuration/memory/index.md) to initialize memory, teach your agent, configure background reflection, and reorganize a hierarchy that has grown over time.
