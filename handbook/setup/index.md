---
title: Set up Letta | Letta Docs
description: Start with the Letta web app or CLI, connect a model provider, and
  choose a setup that fits your workflow.
applies_to:
  backends:
    - cloud
    - local
  interfaces:
    - web
    - cli
---

The **[Letta web app](https://chat.letta.com)** is the quickest way to get started. From one interface, you can create agents, inspect their memory, connect model providers, and choose where their tools run. You can also [install it as a desktop app](/platform/letta-desktop/index.md).

Prefer working in a terminal, or want agents stored only on your machine? Follow the **[Letta CLI](/platform/cli/index.md)** path instead.

## Path 1: Letta web app

The web app works with agents backed up to your Letta account. Where the agent’s state lives and where its tools execute are separate choices.

### 1. Sign in

Open [chat.letta.com](https://chat.letta.com) and sign in with your Letta account. If you don’t have one, you’ll be prompted to create a free account.

### 2. Connect a model provider

Agents can use Letta Auto, pay-as-you-go models, and supported providers or coding plans connected to your account. They cannot use model servers running only on your local machine.

To connect a provider, open [Preferences > Models](https://chat.letta.com/preferences/models), then choose a model from the model selector.

Plans and model options change over time. See the [pricing and model guide](/pricing/index.md) for current details.

### 3. Choose where tools run (optional)

The web app runs tools in a managed [cloud sandbox](/platform/computers/cloud-sandboxes/index.md) by default. To let the agent read files or run commands on your own machine instead:

1. Install the [Letta CLI](#path-2-letta-cli) on that machine and run `/login`.
2. Run `letta server` and leave it running.
3. In [chat.letta.com](https://chat.letta.com), select the machine from the environment picker.

Permission modes and allow/deny rules determine which actions require confirmation. Review these settings before connecting a machine that contains sensitive files or credentials. See the [remote environments](/platform/computers/byom/index.md) and [permissions](/configuration/permissions/index.md) documentation for details.

## Path 2: Letta CLI

Install Node.js **22.19 or newer**, then install the Letta CLI:

```
npm install -g @letta-ai/letta-code
```

Start the Letta CLI from the directory where you want the agent to work:

```
cd /path/to/your/project
letta
```

On first launch, the Letta CLI creates a local agent without requiring a login. Use `/connect` to add a supported model provider, coding plan, or local inference server:

```
> /connect
```

Run `/login` if you want cloud backup and access to your agents from other devices. Once your model is connected, run `/init` to let the agent inspect the current project and bootstrap its memory:

```
> /init
```

## Quick reference

| Command    | Action                                             | Example              |
| ---------- | -------------------------------------------------- | -------------------- |
| `letta`    | Start interactive terminal mode                    | `letta`              |
| `/connect` | Connect model providers, plans, or local inference | `> /connect`         |
| `/login`   | Sign in with Letta                                 | `> /login`           |
| `/model`   | Switch the active model                            | `> /model`           |
| `/init`    | Bootstrap agent memory for the current project     | `> /init`            |
| `exit`     | Exit the Letta CLI                                 | `> exit` or `Ctrl+C` |

## Next step

Now that you’re set up and a model is connected, create an agent and verify that its memory persists across conversations.

Continue to **[Meet your agent](/handbook/meet-your-agent/index.md)**.
