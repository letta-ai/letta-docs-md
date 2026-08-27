---
title: Set up Letta | Letta Docs
description: Install the Letta app or CLI, connect a model provider, and choose a setup that fits your workflow.
---

The **[Letta app](/platform/desktop-app/index.md)** is the quickest way to get started. From one interface, you can create agents, inspect their memory, connect model providers, and choose where their tools run.

Prefer working in a terminal? Follow the **[Letta CLI](/platform/cli/index.md)** path instead.

## Path 1: Letta app

The desktop app supports both locally stored agents and agents backed up to your Letta account. Where the agent’s state lives and where its tools execute are separate choices.

### 1. Download and install the app

Download the Letta app for your platform:

- [macOS, Apple silicon](https://download.letta.com/mac/dmg/arm64)
- [Windows, x64](https://download.letta.com/windows/nsis/x64)
- [Windows, ARM64](https://download.letta.com/windows/nsis/arm64)
- [Linux, x64 AppImage](https://download.letta.com/linux/appImage/x64)
- [Linux, ARM64 AppImage](https://download.letta.com/linux/appImage/arm64)

Launch the app after installation.

### 2. Choose where your agent’s state lives

Choose whether to continue locally or sign in with Letta when you create an agent:

- **Local mode**: The source of truth for the agent’s memory, context, and message history lives on the current machine. No Letta account is required. You are responsible for backing up local agent state.
- **Sign in with Letta**: The agent’s state is backed up to the cloud and can be accessed from the desktop app, CLI, [chat.letta.com](https://chat.letta.com), and supported remote environments.

You can sign in and still keep local agents on the same machine. Local agents do not appear in the web app or other signed-in services.

### 3. Connect a model provider

Letta supports hosted models, connected providers, coding plans, and local inference:

- **Signed-in agents** can use Letta Auto, pay-as-you-go models, and supported providers or coding plans connected to your account. They cannot use model servers running only on your local machine.
- **Local agents** can use supported providers you connect locally or a local inference server.

To configure a provider:

1. Click **Connect model providers** in the bottom-left menu of the app.
2. Choose a supported provider, coding plan, or local inference option appropriate for your agent’s storage mode.
3. Follow the prompts, then choose a model from the model selector.

Plans and model options change over time. See the [pricing and model guide](/pricing/index.md) for current details.

### 4. Enable remote access (optional)

A remote environment separates where you talk to an agent from where its tools execute. For example, you can chat from your phone while the agent reads files or runs commands on your desktop.

Remote environments require an agent backed up to your Letta account. They do not work with agents stored only in the local backend. The desktop app must also remain running on the machine where you want tools to execute.

To make your desktop available as a remote environment:

1. Open settings inside the desktop app.
2. Enable **Allow remote access**.
3. Open [chat.letta.com](https://chat.letta.com) from another device and select your desktop from the environment picker.
4. Continue the conversation. Shell commands, file access, and other client-side tools now run on the selected desktop.

Permission modes and allow/deny rules determine which actions require confirmation. Review these settings before enabling remote access, especially on a machine that contains sensitive files or credentials. See the [remote environments](/platform/computers/byom/index.md) and [permissions](/configuration/permissions/index.md) documentation for details.

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

Now that the app or CLI is installed and a model is connected, create an agent and verify that its memory persists across conversations.

Continue to **[Meet your agent](/handbook/meet-your-agent/index.md)**.
