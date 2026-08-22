---
title: Quickstart | Letta Docs
description: Get started with the Letta app, CLI, or web app
---

Choose the desktop app, CLI, or web app to get started. The desktop app and CLI can use your existing API keys and coding plans, while the web app runs agents in a cloud sandbox with no local setup.

## Setup

- [Desktop App](#tab-panel-8)
- [CLI](#tab-panel-9)
- [Cloud Agents](#tab-panel-10)

1. **Download and install the Letta app**

   [Download for macOS ](#)

   Available for [macOS (Apple Silicon)](https://download.letta.com/mac/dmg/arm64), [Windows (x64)](https://download.letta.com/windows/nsis/x64), [Windows (ARM64)](https://download.letta.com/windows/nsis/arm64), [Linux (AppImage, x64)](https://download.letta.com/linux/appImage/x64), and [Linux (AppImage, ARM64)](https://download.letta.com/linux/appImage/arm64)

2. **Open the Letta app**

   Launch the app and select “Skip login”.

   Click “Connect model providers” in the bottom-left menu to add external API keys and coding plans.

3. **Select your agent and conversation**

   Brand-new accounts start in Tutor, an onboarding agent. You can also create or switch agents later. To start chatting with an agent, enter the main chat, or create a new conversation.

1) **Install the Letta CLI**

   Run the following command to install the Letta CLI via your terminal (requires [Node.js](https://nodejs.org/en/download) version 22.19+):

   ```
   npm install -g @letta-ai/letta-code
   ```

   To launch the Letta CLI, run:

   ```
   letta
   ```

   If you’re running the Letta CLI interactively for the first time, a Tutor agent will be auto-created for you.

2) **Connect to LLM providers**

   Use `/connect` to connect external API keys, coding plans, and local inference servers.

3) **Navigate to your project**

   ```
   cd your-project
   letta
   ```

4) **Send your first message**

   You’re ready to chat! Try asking your agent to explore your codebase or run `/init` to bootstrap its memory.

   Use `/new` to start a new conversation (or `letta --new`), `/resume` to swap conversations, `/agent` to swap agents, and `/model` to swap models. View the [CLI reference](/platform/cli/reference/index.md) to see the full list of CLI commands.

5) **Optional: sign in with Letta**

   Run `/login` to back up your agents to the cloud and make them available from any device, including [chat.letta.com](https://chat.letta.com). If you continue without an account, your agents are stored only on local disk and may require manual backups.

1. **Open the Letta web app and sign in**

   Visit [chat.letta.com](https://chat.letta.com) from your browser or phone and sign in with your Letta account. If you don’t have one, you’ll be prompted to create a free account.

2. **Select your agent and conversation**

   Brand-new accounts start in Tutor, an onboarding agent. You can also create or switch agents and conversations from the sidebar.

3. **Choose where your agent runs**

   The web app uses a managed [cloud sandbox](/platform/computers/cloud-sandboxes/index.md) by default, so you can start without configuring a computer. To give your agent access to files and tools on your laptop, workstation, or cloud VM, [connect your own machine](/platform/computers/byom/index.md) and select it from the environment picker.

4. **Send your first message**

   You’re ready to chat! Try asking your agent to research a topic, create a file, or run `/init` to bootstrap its memory.

5. **Connect your GitHub (optional)**

   Sync your GitHub org to Letta on the [Integrations](https://chat.letta.com/preferences/integrations) page. By configuring your GitHub, agents in your Letta org running on cloud computers will be able to access your GitHub repos to do work.

6. **Connect your Slack (optional)**

   You can easily bring your Letta agents to Slack with Letta’s native Slack integration. Simply visit an agent that you want to connect to Slack on [chat.letta.com](https://chat.letta.com), then click the `Connections` tab to configure a Slack app for that agent.

## First steps

Try one of the following prompts to get a feel for your agent’s capabilities:

```
> /init
```

```
> What do you know about me so far?
```

```
> Create a user profile on my by looking at my downloads folder
```

```
> What active projects am I working on? Which one do you think you could help with?
```

```
> Re-tool your memory to be just like the AI from the movie Her, operate as my AI OS companion
```

## Customizing your agent

Once you have an agent, start customizing its behavior and capabilities.

### Mods

The Letta agent harness is intentionally minimal so you can add your preferred set of features through [Mods](/configuration/mods/index.md).

Mods are trusted code that let an agent modify the runtime it executes in — adding tools, commands, and UI, or changing how context is fed into the model. Browse the [Mods catalog](https://www.letta.com/agent/mods/) to see what’s available. A few recommended mods to start with:

```
letta install npm:@letta-ai/image-understanding   # vision for text-only models
letta install npm:@letta-ai/memfs-search          # keyword + optional semantic memory search
letta install npm:@letta-ai/plan-mode             # plan-before-execute workflow
```

Run `/reload` after installing to activate a mod.

You can also ask your agent to write custom mods for you - agents are aware of mods and how to create them out of the box.

### Skills

[Skills](/configuration/skills/index.md) are reusable instructions your agent loads when relevant—API patterns, workflows, or specialized procedures. Letta implements the open [Agent Skills](https://agentskills.io) standard, so you can install skills built for other agents, including Hermes (`official/...`) and OpenClaw (`clawhub/...`) skills:

```
letta install official/<skill-name>   # Hermes-style official skill
letta install clawhub:<slug>          # OpenClaw ClawHub skill
```

You can also just ask your agent to install a skill from a GitHub URL, or browse the [Letta skills repo](https://github.com/letta-ai/skills) for ideas.

### Learning

Your agent learns how to behave from you. Give it feedback in plain language (“be more concise”, “always run the tests before committing”) and it will update its memory to match. When it makes a mistake it should never repeat, use `/remember` to make the correction durable:

```
> /remember always use pnpm in this project, never npm
```

Your agent also has full access to all prior conversation data, which it can search via tools, [skills](/configuration/skills/index.md), and [subagents](/configuration/subagents#built-in-subagents/index.md). If you’ve discussed something before, your agent can find it (e.g. “*We definitely fixed a similar bug before, do you remember what the solution was?*”).

## Essential commands

You’ll likely want to use the following essential commands when using the Letta CLI:

| Command            | What it does                                   | Example                                  |
| ------------------ | ---------------------------------------------- | ---------------------------------------- |
| `letta`            | Start interactive mode                         | `letta`                                  |
| `letta -p "query"` | Run a query in headless mode                   | `letta -p "commit the changes and push"` |
| `shift-tab`        | Toggle permission modes                        | Press `Shift+Tab`                        |
| `/init`            | Run deep memory initialization (or re-init)    | `> /init`                                |
| `/doctor`          | Audit and refine memory structure              | `> /doctor`                              |
| `/remember`        | Teach your agent something                     | `> /remember always use pnpm`            |
| `/memory`          | View and manage memory blocks                  | `> /memory`                              |
| `/model`           | Switch the LLM model                           | `> /model`                               |
| `/search`          | Search past messages                           | `> /search auth bug`                     |
| `/clear`           | Clear context window (messages buffer)         | `> /clear`                               |
| `/new`             | Start a new conversation                       | `> /new`                                 |
| `/pin`             | Pin agent for easy access                      | `> /pin`                                 |
| `/agents`          | Swap between agents                            | `> /agents`                              |
| `/feedback`        | Report issues or give feedback                 | `> /feedback`                            |
| `!`                | Enter bash mode to run a bash command directly | `! git status`                           |
| `exit` or `Ctrl+C` | Exit Letta Code                                | `> exit`                                 |

## Next steps

Read more about the agent’s memory, skills, and subagents, which are essential to getting the most out of your agent:

- [Memory](/concepts/memfs/index.md) - Understand the hierarchical memory system
- [Skills](/configuration/skills/index.md) - Create reusable modules to extend your agent
- [Subagents](/configuration/subagents/index.md) - Letta agents can spawn other (sub)agents
- [Scheduling](/configuration/schedules/index.md) - Run one-time or recurring prompts while a remote environment is connected
- [Headless mode](/platform/cli/headless/index.md) - Run Letta Code non-interactively

## Getting help

- **Join our Discord**: The best way to get help is to join our [Discord server](https://discord.gg/letta) and chat with other community members and devs on the Letta team.
- **Ask your agent**: Your agent can browse the web, including these docs!
