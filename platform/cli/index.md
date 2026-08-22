---
title: Letta CLI | Letta Docs
description: Run the Letta CLI from your terminal
---

## Install the Letta CLI

Requires Node.js 22.19+

`npm install -g @letta-ai/letta-code`

![Letta CLI](/letta-code-demo.gif)

## Getting started

1. **Install the Letta CLI**

   Run the following command to install the Letta CLI via your terminal (requires [Node.js](https://nodejs.org/en/download) version 22.19+):

   ```
   npm install -g @letta-ai/letta-code
   ```

   To launch the Letta CLI, run:

   ```
   letta
   ```

   If you’re running the Letta CLI for the first time, a new local agent will be auto-created for you. This default local mode stores agent state on your machine and does not require a Letta login.

   If you have an older version of Node.js installed, `npm install -g` may silently install an older version of Letta Code that is compatible with your Node version. To ensure you get the latest version, make sure your Node.js is 22.19 or newer. You can check with `node --version`.

2. **Connect to LLM providers**

   Use `/connect` to connect external API keys, coding plans, and local inference servers.

3. **Navigate to your project**

   ```
   cd your-project
   letta
   ```

4. **Send your first message**

   You’re ready to chat! Try asking your agent to explore your codebase or run `/init` to bootstrap its memory.

   Use `/new` to start a new conversation (or `letta --new`), `/resume` to swap conversations, `/agent` to swap agents, and `/model` to swap models. View the [CLI reference](/platform/cli/reference/index.md) to see the full list of CLI commands.

5. **Optional: sign in with Letta**

   Run `/login` to back up your agents to the cloud and make them available through `chat.letta.com`, the desktop app, remote machines, and messaging integrations. Free accounts support up to three agents.

You can also run the CLI in [headless mode](/platform/cli/headless/index.md) for automations.
