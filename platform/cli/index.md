---
title: Letta Code CLI | Letta Docs
description: Run the Letta Code CLI from your terminal
applies_to:
  backends:
    - cloud
    - local
  interfaces:
    - cli
---

## Install the Letta Code CLI

Requires Node.js 22.19+

`npm install -g @letta-ai/letta-code`

![Letta Code CLI](/letta-code-demo.gif)

## Getting started

1. **Install the Letta Code CLI**

   Run the following command to install the Letta Code CLI via your terminal (requires [Node.js](https://nodejs.org/en/download) version 22.19+):

   ```
   npm install -g @letta-ai/letta-code
   ```

   Alternatively, install with [uv](https://docs.astral.sh/uv/) or [pipx](https://pipx.pypa.io/) (Node.js is bundled):

   Terminal window

   ```
   uv tool install letta
   # or
   pipx install letta
   ```

   Requires Python 3.9+. Wheels support glibc Linux 2.28+ (x86-64/ARM64), macOS 14+ (Intel/Apple Silicon), and Windows x64; Alpine/musl, 32-bit systems, and Windows ARM64 are unsupported.

   If `npm install -g` fails with `EACCES`, don’t use `sudo`: root ownership prevents the CLI’s `npm install -g` self-updates. Use uv/pipx, a user-owned npm prefix, or nvm.

   To launch the Letta Code CLI, run:

   ```
   letta
   ```

   If you’re running the Letta Code CLI for the first time, a new local agent will be auto-created for you. This default local mode stores agent state on your machine and does not require a Letta login.

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

   Run `/login` to back up your agents to the cloud and make them available through `chat.letta.com`, remote machines, and messaging integrations. Free accounts support up to three agents.

You can also run the CLI in [headless mode](/platform/cli/headless/index.md) for automations.
