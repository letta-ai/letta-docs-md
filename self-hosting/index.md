---
title: Self-hosting | Letta Docs
description: Store agents locally or on infrastructure you control
---

Letta agents can run entirely on infrastructure you control, in two shapes:

- **Local runtime**: The CLI runs agents in-process. The desktop app uses a background App Server on your machine. In both cases, all agent state, including messages, memory, and provider connections, stays on-device, and no Letta account is required.
- **Self-hosted App Server**: Run the Letta App Server to host local agents on a central, always-on machine and expose them to client applications through the [Agent SDK](/agent-sdk/index.md). Run messaging channels in a separate server process on the same machine.

**Limitations of self-hosting:** Built-in tools run where the agent harness runs: on the local machine for the CLI and desktop app, or on the machine running App Server. When you connect through the Agent SDK, [client tools and MCP tools](/agent-sdk/mcp/index.md) can instead run through the SDK host or a configured MCP server. Self-hosted agents cannot be accessed through chat.letta.com and are not automatically backed up. Back up their state manually if you need to preserve or move it.

## Setup

- [App Server](#tab-panel-13)
- [CLI](#tab-panel-14)
- [Desktop App](#tab-panel-15)

1. **Install the Letta CLI**

   Run the following command to install the Letta CLI via your terminal (requires [Node.js](https://nodejs.org/en/download) version 22.19+):

   ```
   npm install -g @letta-ai/letta-code
   ```

2. **Connect model providers**

   Connect the model providers you want your agents to use, for example a locally running Ollama server:

   ```
   letta --backend local connect ollama
   ```

   You can also connect external API keys or other local inference servers:

   ```
   letta --backend local connect anthropic --api-key "$ANTHROPIC_API_KEY"
   letta --backend local connect lmstudio --base-url http://127.0.0.1:1234/v1
   ```

   See [Models](/configuration/models/index.md) for the full list of supported providers.

3. **Run the Letta server**

   Start the [App Server](/platform/app-server/index.md) with the local backend:

   ```
   letta server --backend local --listen ws://127.0.0.1:4500
   ```

   The process prints the base URL and channel URLs at startup. See the [App Server quickstart](/platform/app-server/quickstart/index.md) for authentication and configuration options.

4. **Add channels (optional)**

   To make your agents reachable through messaging platforms, start a separate local server process with one or more [channels](/configuration/channels/index.md):

   ```
   letta server --backend local --channels slack
   ```

   See the channel-specific guides for setup instructions, e.g. [Slack](/configuration/channels/slack/index.md), [Telegram](/configuration/channels/telegram/index.md), or [Discord](/configuration/channels/discord/index.md).

5. **Connect via the SDK (optional)**

   Connect to the running server from your application with the [Letta Agent SDK](/agent-sdk/index.md)’s remote backend:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   const client = new LettaAgentClient({
     backend: "remote",
     url: "http://127.0.0.1:4500",
   });
   ```

   See the [Agent SDK](#agent-sdk) section below for a full example.

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

1. **Download and install the Letta app**

   [Download for macOS ](#)

   Available for [macOS (Apple Silicon)](https://download.letta.com/mac/dmg/arm64), [Windows (x64)](https://download.letta.com/windows/nsis/x64), [Windows (ARM64)](https://download.letta.com/windows/nsis/arm64), [Linux (AppImage, x64)](https://download.letta.com/linux/appImage/x64), and [Linux (AppImage, ARM64)](https://download.letta.com/linux/appImage/arm64)

2. **Open the Letta app and connect models**

   Launch the app and select “Skip login” (this will store agents locally).

   Click “Connect model providers” in the bottom-left menu to add external API keys, coding plans, or locally running model endpoints.

Model inference is a separate choice. If you connect a remote model provider, prompts still go to that provider. To keep inference local too, connect a local provider such as Ollama, LM Studio, or llama.cpp. See [Local models](/configuration/models#local-models/index.md) for both local and cloud-hosted setup options.

## Agent SDK

The [Letta Agent SDK](/agent-sdk/index.md) supports two backends for self-hosted setups:

- **Local backend** (`backend: "local"`): The SDK starts [App Server](/platform/app-server/index.md) automatically as a subprocess on the current machine. Agent state and the execution environment stay on the machine running your code. Use this for development or single-machine deployments—no separate server process to manage.
- **Remote backend** (`backend: "remote"`): The SDK connects to an App Server you run as a separate service (`letta server --listen`). Agent state and the execution environment live on the App Server machine, so multiple clients can share the same agents and the server can run on different infrastructure than your application.

* [Local backend](#tab-panel-11)
* [Remote backend](#tab-panel-12)

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({ backend: "local" });


const agentId = await client.createAgent({
  persona: "You are Patch, a resident engineering teammate for this repository.",
});


await using session = client.createSession(agentId, {
  cwd: process.cwd(),
});


await session.send("Inspect this repository and write an onboarding memo.");


for await (const message of session.stream()) {
  if (message.type === "assistant") {
    console.log(message.content);
  }
}
```

Start an App Server on the machine that should hold agent state:

```
letta server --backend local --listen ws://127.0.0.1:4500
```

Then connect to it from your application:

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "remote",
  url: process.env.LETTA_APP_SERVER_URL ?? "http://127.0.0.1:4500",
  authToken: process.env.LETTA_APP_SERVER_TOKEN,
});


const agentId = await client.createAgent({
  persona: "You are Ops, a digital employee running in a shared workspace.",
});


await using session = client.createSession(agentId, {
  cwd: "/workspace/project",
});


await session.send("Prepare a morning handoff report for the workspace.");


for await (const message of session.stream()) {
  if (message.type === "assistant") {
    console.log(message.content);
  }
}
```

See the [Agent SDK docs](/agent-sdk/index.md) for full setup instructions and [Deployment](/agent-sdk/deployment/index.md) for production configurations.

For OpenAI-compatible clients, see the [App Server quickstart](/platform/app-server/quickstart#openai-compatible-api/index.md).

## Deployment

To make a self-hosted Letta server accessible to a client-side application, deploy [App Server](/platform/app-server/index.md) as a standalone service on infrastructure you control (a VM, container, or on-prem machine) and connect to it with the SDK’s remote backend.

1. **Start App Server on the host machine**

   Use the local backend so agent state stays on the server, and bind to a non-loopback address so other machines can reach it:

   ```
   letta server --backend local --listen ws://0.0.0.0:4500
   ```

   Installing the Letta CLI compiles native dependencies, so minimal Linux images and fresh VPSes need Python and a C++ toolchain first. On Debian/Ubuntu (including the `node:22-slim` Docker image), install them before `npm install -g @letta-ai/letta-code`:

   ```
   apt-get install -y python3 make g++
   ```

2. **Configure authentication**

   Non-loopback listeners should require WebSocket auth. Capability-token auth reads a token from a file and requires clients to send it as a bearer token:

   ```
   letta server \
     --backend local \
     --listen ws://0.0.0.0:4500 \
     --ws-auth capability-token \
     --ws-token-file /absolute/path/to/app-server-token
   ```

   You can also use signed bearer tokens with `--ws-auth signed-bearer-token` and `--ws-shared-secret-file /absolute/path/to/secret`.

3. **Connect from your application**

   Point the SDK at the server’s URL and pass the auth token:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   const client = new LettaAgentClient({
     backend: "remote",
     url: process.env.LETTA_APP_SERVER_URL, // e.g. "http://your-server:4500"
     authToken: process.env.LETTA_APP_SERVER_TOKEN,
   });
   ```

   Agent state and tool execution stay on the App Server machine; multiple clients can connect to the same server and share its agents.

App Server has filesystem and shell access on the machine where it runs. Never expose it directly to untrusted clients or embed its auth token in browser code—route client-side applications through your own backend, which holds the token and talks to App Server on their behalf.

For protocol details, lifecycle management, and lower-level integration options, see the [App Server docs](/platform/app-server/index.md) and [Deployment](/agent-sdk/deployment/index.md).

## Where local state is stored

By default, local state is stored in:

```
~/.letta/lc-local-backend
```

Each agent’s MemFS repository is stored under:

```
~/.letta/lc-local-backend/memfs/<agent-id>/memory
```

Use `LETTA_LOCAL_BACKEND_DIR` to isolate local state for a project or experiment:

```
export LETTA_LOCAL_BACKEND_DIR="$PWD/.letta-local"
letta --backend local --new-agent
```

Add `.letta-local/` to `.gitignore` if you create it inside a repository.

## Troubleshooting

### My prompts are still going to a remote provider

Local setup stores agent state locally, but inference follows the model provider you selected. Switch to an Ollama, LM Studio, or llama.cpp model to run inference locally.

### My local model does not appear in `/model`

Make sure the local inference server is running, then reconnect the provider:

```
letta --backend local connect ollama
letta --backend local connect lmstudio --base-url http://127.0.0.1:1234/v1
```

### I want a clean local setup for testing

Set `LETTA_LOCAL_BACKEND_DIR` to a temporary directory before launching Letta Code:

```
export LETTA_LOCAL_BACKEND_DIR="$(mktemp -d)"
letta --backend local --new-agent
```
