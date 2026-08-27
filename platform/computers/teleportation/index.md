---
title: Teleportation | Letta Docs
description: Move an active conversation from one computer to another
---

**Teleportation** moves an active conversation to a different computer. The agent keeps its memory and message history, and continues the task on the new computer.

Use it when the work outgrows where it started. Hand a long build from your laptop to a cloud sandbox, or move a conversation out of a sandbox onto the machine that already has the repository and credentials it needs.

## Move a conversation

Tell the agent where to continue, such as “finish this in the cloud” or “move to my work laptop”. The agent transfers the files the destination needs, teleports as its last action on the current computer, then picks the task back up there.

You can also move a conversation yourself with the environment picker under the chat window. The picker is the only way to bring a conversation back to **Local**, which an agent cannot do on its own.

## What moves

| Moves with the conversation                        | Stays on the computer                 |
| -------------------------------------------------- | ------------------------------------- |
| Agent memory and [MemFS](/concepts/memfs/index.md) | Files and working directories         |
| Message history                                    | Running processes and services        |
| Pending tool approvals                             | Credentials and environment variables |
| Permission mode                                    | Installed software and dependencies   |

Paths do not transfer. After arriving, the agent sets up its working directory again: clone or check out the repository, install dependencies, and restart anything it was running.

Teleporting away from a [cloud sandbox](/platform/computers/cloud-sandboxes/index.md) does not delete it. The conversation keeps the same sandbox, so files left there are still available if the agent teleports back.

## Requirements

- The agent’s state lives in Letta Cloud. Agents on a local backend cannot teleport.
- Both computers are online and running Letta Code 0.30.20 or later.
- A conversation can have only one teleport in flight at a time.
- The destination is a cloud sandbox or a [connected machine](/platform/computers/byom/index.md). Moving back to **Local** is done from the environment picker.

## How it works

1. Letta Cloud checks that both computers are online and can hand off the conversation, then asks the source computer to release it.

2. The source finishes the tool call it is running, stops taking new work for that conversation, and hands back whatever the agent was waiting on.

3. Letta Cloud starts the conversation on the destination and delivers the handoff, including a pending tool approval if there was one.

4. The destination becomes the conversation’s computer, and the agent continues without a new prompt.

If a step fails, for example the destination goes offline partway through, the conversation stays on the source computer and the agent reports what went wrong.
