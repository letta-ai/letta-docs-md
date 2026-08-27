---
title: Computers | Letta Docs
description: Choose where Letta agents run tools and access files
---

A **computer** is the execution environment where a Letta agent runs shell commands, reads and writes files, and uses local tools. The agent’s identity and memory are separate from the computer, so a signed-in agent can move between environments without losing what it knows.

## Choose an environment

| Environment                                                   | Best for                                             | Setup                                     |
| ------------------------------------------------------------- | ---------------------------------------------------- | ----------------------------------------- |
| Current computer                                              | Working directly with local files and tools          | Use the desktop app or CLI                |
| [Cloud sandbox](/platform/computers/cloud-sandboxes/index.md) | Quick tasks in an isolated managed environment       | Selected automatically in the web app     |
| [Your own remote machine](/platform/computers/byom/index.md)  | Long-running work or access to a specific filesystem | Connect the machine to your Letta account |

## Current computer

The desktop app and CLI can run tools directly on the machine in front of you. The agent sees the working directory you select and uses that machine’s shell, files, credentials, and installed software, subject to your permission settings.

## Cloud sandboxes

A [cloud sandbox](/platform/computers/cloud-sandboxes/index.md) is provisioned for you and requires no local setup. It is useful for isolated work and tasks started from the web app.

## Bring your own machine

Connect a laptop, workstation, VM, or container when you want to access its files and tools remotely. See [Bring your own machine](/platform/computers/byom/index.md) for setup.

## Teleportation

An active conversation can move from one computer to another and continue where it left off. See [Teleportation](/platform/computers/teleportation/index.md).

An agent can only access the files, commands, and credentials available in its current environment. Moving an agent does not copy a project directory or local secrets to the new computer.
