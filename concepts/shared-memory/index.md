---
title: Shared memory | Letta Docs
description: Share Git-backed files between cloud-hosted Letta agents
---

Shared memory gives multiple agents access to the same files and working context. Each shared memory repository is a Git repository hosted in Letta Cloud and owned by your organization.

Older Letta API guides use **shared memory blocks** for one in-context memory block attached to multiple agents. The legacy memory block API still supports this pattern, but users should migrate to shared memory repositories instead.

| Memory                            | Ownership         | Use                                                      |
| --------------------------------- | ----------------- | -------------------------------------------------------- |
| [MemFS](/concepts/memfs/index.md) | One agent         | Store the agent’s identity, skills, and long-term memory |
| Shared memory repository          | Your organization | Share knowledge and working files between agents         |

Use shared memory for team conventions, product knowledge, research, plans, and documents that multiple agents maintain.

## How agents access shared memory

Attach a repository to each agent that needs it. The agent’s system prompt lists the repository path and its top-level files. Letta Code clones the repository beside the agent’s MemFS at:

```
$MEMORY_DIR/../<repository-name>/
```

The agent reads and edits the repository with normal file and Git tools. The agent must commit and push its changes. Other agents can then pull those commits into their own checkouts.

An attached repository can also provide skills to its agents. Put each skill in `skills/<skill-name>/SKILL.md` at the repository root. Letta Code stops loading these skills when you detach the repository.

Letta Code clones a repository when it first becomes available. Later synchronization fast-forwards the local checkout from its remote. Use `letta shared-memory sync` to pull attached repositories or create a missing checkout.

## Manage shared memory

You can create new shared memories with:

Terminal window

```
letta shared-memory create --name team-memory
```

Attach a shared memory to each agent with the `attach` subcommand:

Terminal window

```
letta shared-memory attach team-memory --agent <agent-id>
letta shared-memory attach team-memory --agent <other-agent-id>
```

The web and desktop apps can also create and attach shared memories. Applications can manage persistent repository attachments with the [Agent SDK](/agent-sdk/repositories/index.md).

Cloud agents can also use the bundled `managing-shared-memory` skill to create, attach, detach, synchronize, and inspect repository history.

Shared memory repositories require cloud-hosted agents. Local agents use their own MemFS and project files.
