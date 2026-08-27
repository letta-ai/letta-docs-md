---
title: Cloud sandboxes | Letta Docs
description: Run a Letta agent in an isolated computer managed by Letta
---

A **cloud sandbox** is an isolated computer provisioned for a Letta agent session. It gives the agent a shell and filesystem without requiring you to configure a local or remote machine.

Cloud sandboxes are the default execution environment for agents started from [chat.letta.com](https://chat.letta.com). They are also available through the Agent SDK when you create a cloud session without selecting another environment.

## What runs in the sandbox

The sandbox is where the agent:

- Runs shell commands
- Reads and writes working files
- Installs dependencies
- Uses computer-scoped tools

The agent’s identity, conversations, and [MemFS](/concepts/memfs/index.md) remain with the agent rather than the sandbox.

## Files and lifecycle

A cloud sandbox has its own filesystem. Paths on your laptop are not mounted automatically, so upload or clone the files the agent needs inside the sandbox.

A conversation can [teleport](/platform/computers/teleportation/index.md) out of its sandbox and back. The sandbox is not deleted when the conversation leaves, so files stay where the agent left them.

Web sessions manage sandbox startup for you. Agent SDK sessions can control the requested TTL, startup timeout, refresh interval, and whether the sandbox terminates when the session closes. See [Agent SDK deployment](/agent-sdk/deployment#managed-sandboxes/index.md) for those options.

## When to bring your own machine

Use [your own machine](/platform/computers/byom/index.md) instead when the task needs an existing local checkout, private network access, specialized hardware, or software that is already configured on that computer.
