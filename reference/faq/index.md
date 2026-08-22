---
title: Frequently asked questions | Letta Docs
description: Answers to common questions about Letta apps, the CLI, App Server, memory, tools, and troubleshooting
---

If you can’t find the answer to your question, join our [Discord](https://discord.gg/letta) and ask there!

## Web app (chat.letta.com)

### How can I use the web app with local agents?

The web app works only with agents hosted in Letta Cloud. You can still run those agents on your own computer: install the Letta CLI or desktop app, sign in, and select the agent. The agent’s state remains in Letta Cloud while its tools run on the computer where you started the CLI or app.

To build your own web app for agents stored on your device, use the [Letta Agent SDK](/agent-sdk/index.md) with a [self-hosted App Server](/self-hosting/index.md). Authenticated browser clients need a trusted backend or WebSocket proxy between the browser and App Server.

## Desktop app

### Does the desktop app connect to remote App Servers?

No. The desktop app currently supports two backends:

- **Letta Cloud:** Agent state is stored in Letta Cloud, while tools can run on the current computer or a [connected computer](/platform/computers/index.md).
- **Local:** Agent state and tools stay on the computer running the desktop app.

The desktop app does not currently accept a self-hosted App Server URL.

If you are deploying a remote App Server and want a rich UI, you can:

- Enable its [OpenAI-compatible API](/platform/app-server/quickstart#openai-compatible-api/index.md) and connect a frontend such as [Open WebUI](https://openwebui.com/).
- Use the [`letta-acp` adapter](/platform/acp/index.md) with an ACP client such as [Zed](https://zed.dev/ai) or [Buzz](https://buzz.xyz/).
- Build a custom frontend with the [Letta Agent SDK](/agent-sdk/index.md).

The [`letta-oss-ui`](https://github.com/letta-ai/letta-oss-ui) repository is an open-source Electron chat UI built with the Letta Agent SDK. It supports Letta Cloud, fully local agents, and self-hosted App Servers.

## CLI

### Can I connect the CLI to a remote App Server?

No. Like the desktop app, the CLI supports agents hosted in Letta Cloud and local agents stored on the same machine as the CLI. It does not currently accept a self-hosted App Server URL.

For a remote App Server using the local backend, SSH into that machine and run `letta` there to use the same locally stored agents.

## App Server

### What port does App Server run on?

A bare `letta server --listen` command binds to `127.0.0.1` on an automatically selected available port. The CLI prints the selected address and WebSocket endpoint when it starts.

If you need a stable port, specify it explicitly:

Terminal window

```
letta server --listen ws://127.0.0.1:4500
```

This listens on port `4500`, with the WebSocket available at `ws://127.0.0.1:4500/ws`. Port `4500` is an example, not a fixed default. See the [App Server quickstart](/platform/app-server/quickstart/index.md) for startup and authentication options.

### Is there a REST API?

The native App Server API is its bidirectional WebSocket protocol. For clients that expect an HTTP API, start App Server with the built-in [OpenAI-compatible API](/platform/app-server/quickstart#openai-compatible-api/index.md):

Terminal window

```
letta server --listen ws://127.0.0.1:4500 --openai-api
```

This exposes OpenAI-compatible Models, Chat Completions, and Responses endpoints alongside the native `/ws` endpoint. The compatibility API is useful for existing OpenAI clients, but it does not expose the full App Server lifecycle, event stream, approval flow, or management protocol.

Agents hosted in Letta Cloud are also accessible through the Letta REST API using a `LETTA_API_KEY`. However, developers building agent applications should use the [Letta Agent SDK](/agent-sdk/index.md), not the lower-level REST API or generated client SDKs. The Agent SDK manages the harness, tools, execution environment, streaming, and sandbox lifecycle.

### How do I keep Open WebUI chats in separate Letta conversations?

Set [`ENABLE_FORWARD_USER_INFO_HEADERS=true`](https://docs.openwebui.com/reference/env-configuration/#enable_forward_user_info_headers) on the Open WebUI process or container, not App Server. Open WebUI then sends `X-OpenWebUI-Chat-Id` on streaming Chat Completions requests. App Server uses that value to route each Open WebUI chat to its own Letta conversation.

## Agent SDK

### What is the difference between the Letta Agent SDK and the Letta client SDK?

The Letta Agent SDK (`@letta-ai/letta-agent-sdk`) is a high-level TypeScript interface to the Letta agent harness. It manages sessions, turns, streaming, approvals, local tools, and execution environments across four deployment patterns: a fully local runtime, a self-hosted App Server, Letta Cloud with managed sandboxes, and Letta Cloud with a connected computer.

The Letta client SDKs—`@letta-ai/letta-client` on npm and `letta-client` on PyPI—are generated, lower-level wrappers around the Letta REST API. The Agent SDK uses the TypeScript client internally when its backend is Letta Cloud, but application developers should not build directly on the generated client SDKs.

Use the Agent SDK for new integrations. It provides the complete harness behavior, including MemFS synchronization, skills, subagents, permission handling, local tool execution, and sandbox or computer lifecycle management.

### Is there a Python version of the SDK?

No. The Letta Agent SDK is currently available only for TypeScript.

We strongly recommend using the TypeScript Agent SDK. When Python is a hard requirement, run App Server separately and connect to its [WebSocket protocol](/platform/app-server/protocol-lifecycle/index.md) with a Python WebSocket library. The TypeScript Agent SDK is fully [open source](https://github.com/letta-ai/letta-agent-sdk) and can serve as a reference implementation.

### Does the Letta Agent SDK support AgentFile (`.af`)?

Not directly. The Agent SDK does not currently expose AgentFile import or export methods.

For agents hosted in Letta Cloud, import an [AgentFile](/v1-sdk/concepts/agent-file/index.md) with `letta --import path/to/agent.af`, then pass the imported agent ID to the Agent SDK. AgentFile import and export are not currently supported by the Agent SDK’s fully local backend or by a self-hosted App Server using the local backend.

## Miscellaneous

### Does MemFS or a Letta agent’s memory support semantic or vector search?

MemFS does not include a semantic or vector index by default. It is a git-tracked collection of Markdown files that the agent searches with normal file-search and read tools. For keyword search and optional semantic or hybrid search, install the [MemFS Search mod](https://github.com/letta-ai/mods/tree/main/packages/memfs-search). Semantic and hybrid modes require [QMD](https://github.com/tobi/qmd).

Conversation-history search is separate from MemFS. On Letta Cloud, `letta messages search` supports full-text, vector, and hybrid search over messages. Local backends currently search conversation transcripts with full-text matching only. See [Semantic and vector search](/concepts/memfs#semantic-and-vector-search/index.md) for details.

### Is there a mobile app for Letta?

There is currently no official native Letta mobile app for iOS or Android.

We recommend using [chat.letta.com](https://chat.letta.com) on your mobile device; it is fully mobile-compatible. You can also build a mobile app with the [Letta Agent SDK’s browser and React Native client](/agent-sdk/browser/index.md).

### Is web search built into Letta agents, the CLI, and the app?

Agents created in Letta Cloud through the Letta CLI or apps include the `web_search` and `fetch_webpage` tools by default. They also have access to a built-in image-generation skill—ask the agent to generate an image, and it will load the skill when needed.

Local agents do not include managed model credentials or built-in web-search and image-generation services. You must connect a model provider and add any additional capabilities yourself. You can do this with skills, MCP servers, or mods; the [web search mod](https://github.com/letta-ai/mods/tree/main/packages/web-search) is one example.

### How can I add custom tools to my agent?

There are several ways to extend an agent. For most use cases, such as teaching an agent to use an additional API or service, we recommend [skills](/configuration/skills/index.md). Skills are easy to install, load only when relevant, and do not permanently expand the agent’s base toolset.

When you need a tool to be available directly to the model, add a session-scoped client tool with the [Letta Agent SDK](/agent-sdk/mcp/index.md) or create a trusted local [mod](/configuration/mods/index.md). See the [web search mod](https://github.com/letta-ai/mods/tree/main/packages/web-search) for an example of adding tools through a mod.

The Agent SDK also supports client-side MCP. Pass stdio, HTTP, or SSE servers through the session’s `mcpServers` option; the SDK discovers their tools and runs the connections in your application’s Node.js process. See [MCP and client tools](/agent-sdk/mcp/index.md) for configuration examples. When possible, we recommend skills over MCP—you can also use a skill such as [`mcp-cli`](https://github.com/philschmid/mcp-cli) to access an MCP server through its CLI.

### Why does my agent’s context window keep changing?

Use `/context-limit` in the CLI or app to set a custom context-window limit. Selecting a different model—or a different context-window variant of the same model—resets the limit to that model’s recommended preset. Run `/context-limit` again if you want to restore a custom value after switching models.

### I’m getting a 409 ‘conversation is busy’ error

This error means another run is already active on the same Letta Cloud conversation. The CLI and app normally recover by waiting for that run and retrying or resuming the stream automatically.

Repeated errors can mean that multiple clients or `letta server` processes are sending turns to the same conversation. Close any duplicate clients and let the active run finish. If the conversation remains stuck, restart the affected client.

If you still cannot recover, report the issue with the `/feedback` command.

### I’m getting a ‘No tool call is currently awaiting approval’ error

This error means the client sent an approval response or tool result for a call that the Letta API no longer considers pending. It can happen after a dropped connection, a duplicated response, or another client resolving the same approval first. The CLI and app normally recover automatically.

If the error repeats, close duplicate clients and restart the affected CLI or desktop app so it can reload the conversation’s current state. If you still cannot recover, report the issue with the `/feedback` command.
