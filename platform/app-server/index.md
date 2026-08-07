---
title: Letta App Server | Letta Docs
description: Run a Letta agent runtime for local and remote SDK sessions
---

The recommended way to interface with the App Server is the [Letta Agent SDK](/agent-sdk/index.md), which provides a high-level interface over its WebSocket protocol.

Alternatively, use the App Server’s [OpenAI-compatible API](/platform/app-server/quickstart#openai-compatible-api/index.md) with clients such as Open WebUI, or the [ACP adapter](/platform/acp/index.md) with ACP clients such as Zed.

The **Letta App Server** lets you deploy the Letta agent harness as a service. Whereas [headless mode](/platform/cli/headless/index.md) allows you to interface with Letta agents by spinning up the agent harness as a one-time ephemeral process, the App Server is an always-on service and can manage running multiple agents in parallel in a single process.

You can interact with agents running on the Letta App Server through the Letta Agent SDK or directly through its WebSocket protocol.

The [Letta app](/platform/desktop-app/index.md) uses the App Server under the hood: the desktop app is a client that communicates over WebSockets with a background App Server process, which runs the agent harness and executes tools.

## When to use App Server

### Enabling additional remote environments for cloud-hosted agents

If you are using agents hosted in Letta Cloud, you can use the App Server to create a “remote environment” which your agents can connect to. For example, if you want your agents to be able to access a GPU cluster to run LLM training experiments, you can simply run the App Server command (`letta server`) in the cluster, and it will be available as a remote environment (the alternative would be to give your agent credentials via [secrets](/configuration/secrets/index.md) so that it can SSH in).

For more information on registering remote environments with Letta Cloud, see [Bring your own machine](/platform/computers/byom/index.md).

### Enabling programmatic remote access for self-hosted (local) agents

If you are running Letta fully locally (your agent state is stored on local disk instead of on Letta Cloud), you can use the Letta App Server to enable interacting with your agents over a remote connection. For example, if you run the App Server on a remote VPC and use the `local` App Server backend, you can expose agents stored on the VPC remotely to external clients (e.g. a web app, or a UI running on your local laptop).

### Understanding local vs cloud-hosted agent state

Where an agent’s state is stored can be different from its execution environment (where the harness runs). The `backend` mode of the App Server refers to where the agent state is stored, either in Letta Cloud (`cloud`) or on the local machine (`local`).

When you use Letta Cloud, your agents’ state (message history and memories) is stored in the cloud. This is what enables easy access or “teleportation” of the same agent to and from any device. When you use the Letta app or CLI, you are creating an execution environment that your cloud-hosted agent can run in - your agent will run commands that execute on your local machine, but the state of the agent is stored in the cloud. Similarly, running the App Server to [bring your own machine](/platform/computers/byom/index.md) is another way to create an execution environment for your agent, and the agent state is *not* stored on the same device as the App Server.

When you use Letta’s local backend mode, your agents’ state is stored locally on the same disk where you run the agent harness. That means when running the App Server with the `local` backend, the App Server will read and write the agent state from the local `~/.letta/lc-local-backend` directory.

## How it works

The `letta server --listen [url]` process exposes one bidirectional WebSocket at `/ws`. Clients send commands and receive responses, approvals, tool callbacks, agent output, and runtime state updates over that same connection.

App Server accepts multiple concurrent clients. A client subscribes its connection to an agent and conversation by sending `runtime_start`; one connection can subscribe to multiple runtimes, and multiple connections can subscribe to the same runtime. Runtime-scoped events are sent only to subscribed clients.

The server owns agent execution, tool preparation, turn queueing, and event streaming. Your application owns product state such as users, tasks, dashboards, durable results, and retry policy. See [Protocol lifecycle](/platform/app-server/protocol-lifecycle/index.md) for the command and event flow, and [Integration patterns](/platform/app-server/integration-patterns/index.md) for controller architecture guidance.

## Direct protocol access

For most application integrations, start with the [Letta Agent SDK quickstart](/agent-sdk/quickstart/index.md). It provides high-level APIs for agents, sessions, turns, streaming, and approvals.

For direct TypeScript integrations, use the App Server client exported by `@letta-ai/letta-code` rather than constructing wire messages yourself. The helper opens the WebSocket, correlates `request_id` responses, subscribes runtimes, and tracks turn completion. See the [App Server quickstart](/platform/app-server/quickstart/index.md) for the connection and turn APIs.

The [Remote client API](/agent-sdk/remote-client/index.md) reaches a remote environment through Letta’s hosted router instead of connecting directly to `letta server --listen`. It carries the same runtime commands and events, with hosted discovery, authentication, and transport acknowledgements around them.

## Next steps

- [Letta Agent SDK](/agent-sdk/quickstart/index.md) - Build an application with the recommended high-level interface.
- [App Server quickstart](/platform/app-server/quickstart/index.md) - Operate App Server separately or connect to it directly.
- [Protocol lifecycle](/platform/app-server/protocol-lifecycle/index.md) - Understand runtime startup, turns, sync, and abort.
- [External tools](/platform/app-server/external-tools/index.md) - Register tools that execute in your controller.
- [Integration patterns](/platform/app-server/integration-patterns/index.md) - Design robust controllers and multi-agent services.
