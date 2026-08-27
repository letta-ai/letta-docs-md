---
title: Use Letta with ACP | Letta Docs
description: Connect Letta to clients through the Agent Client Protocol
---

[`letta-acp`](https://github.com/letta-ai/letta-acp) exposes a stateful Letta agent through the [Agent Client Protocol](https://agentclientprotocol.com) (ACP), so any ACP-compatible client can drive it. Code editors are one common way to use ACP, but test harnesses and command-line clients such as [`acpx`](https://github.com/openclaw/acpx) can use the same adapter.

Each ACP session becomes a conversation on a Letta agent. Set `LETTA_AGENT_ID` to reuse an existing agent—and its memory—across clients and sessions. Configure your ACP client to launch the adapter with `npx -y @letta-ai/letta-acp` over stdio.

## Use ACP in an editor

Editors with ACP support can launch `letta-acp` as a custom agent. The following examples cover Zed, JetBrains IDEs, and Obsidian; other ACP clients use the same adapter and environment variables.

### Connect Zed

Run `letta`, enter `/login` in the CLI, then add the adapter to Zed’s settings. Replace `agent-...` with an existing agent ID, or remove `LETTA_AGENT_ID` to create an agent on first use.

\~/.config/zed/settings.json

```
{
  "agent_servers": {
    "Letta": {
      "type": "custom",
      "command": "npx",
      "args": ["-y", "@letta-ai/letta-acp"],
      "env": {
        "LETTA_ACP_BACKEND": "cloud-oauth",
        "LETTA_AGENT_ID": "agent-..."
      }
    }
  }
}
```

Restart Zed, open the Agent Panel, select **+**, and choose **Letta**. External agents appear in this menu, not the model dropdown. The `"type": "custom"` field is required.

If Zed cannot find `npx`, replace it with the absolute path returned by `which npx`. Apps launched from the macOS Dock may not inherit your shell’s `PATH`.

If you let the adapter create an agent, copy its `agent-*` ID from Zed’s ACP logs into `LETTA_AGENT_ID` to keep using it after adapter restarts. Open the logs from the command palette with `dev: open acp logs`.

### Connect JetBrains IDEs

JetBrains IDEs that support custom ACP agents—including WebStorm—can run the same adapter. Run `letta`, enter `/login` in the CLI, then open the **AI Chat** tool window and select **Add Custom Agent**. JetBrains creates `~/.jetbrains/acp.json`; add the following configuration:

\~/.jetbrains/acp.json

```
{
  "default_mcp_settings": {},
  "agent_servers": {
    "Letta": {
      "command": "npx",
      "args": ["-y", "@letta-ai/letta-acp"],
      "env": {
        "LETTA_ACP_BACKEND": "cloud-oauth",
        "LETTA_AGENT_ID": "agent-..."
      }
    }
  }
}
```

Select **Letta** from the agent picker in AI Chat. ACP agents do not require a JetBrains AI subscription. If Letta does not appear or `npx` cannot be started, use the absolute path returned by `which npx` and restart the IDE. This flow has been tested with WebStorm.

### Connect Obsidian

Install and enable the third-party [Agent Client](https://rait-09.github.io/obsidian-agent-client/getting-started/) community plugin. Run `letta`, enter `/login` in the CLI, then open **Settings → Agent Client → Custom Agents** and select **Add custom agent**.

Use these values:

| Field                 | Value                                                                        |
| --------------------- | ---------------------------------------------------------------------------- |
| Agent ID              | `letta`                                                                      |
| Display name          | `Letta`                                                                      |
| Path                  | `npx`                                                                        |
| Arguments             | `-y` and `@letta-ai/letta-acp`, one per line                                 |
| Environment variables | `LETTA_ACP_BACKEND=cloud-oauth` and `LETTA_AGENT_ID=agent-...`, one per line |

Replace `agent-...` with the agent you want to use, or omit that line to create an agent on first use. Open the Agent Client chat view and select **Letta** from the agent menu. The plugin starts the adapter with your vault as its working directory, so `cloud-oauth` lets the agent use local tools against your notes without storing an API key in Obsidian settings.

If Agent Client cannot find `npx`, use the absolute path returned by `which npx` as the **Path** value.

## Choose where tools run

`LETTA_ACP_BACKEND` controls where agent state is stored and where built-in tools such as `Read` and `Bash` execute.

| Backend           | Agent state                   | Built-in tools run | Auth                         |
| ----------------- | ----------------------------- | ------------------ | ---------------------------- |
| `cloud-oauth`     | Letta Platform                | your machine       | `/login` in the Letta CLI    |
| `cloud`           | Letta Platform                | cloud sandbox      | `LETTA_API_KEY`              |
| `local` (default) | your machine                  | your machine       | local model setup            |
| `remote`          | configured by your App Server | App Server machine | capability token, if enabled |

For work in a local repository, `cloud-oauth` is usually the best fit: the agent and its memory stay on the Letta Platform while tools run against the working tree on your machine. It also uses your existing Letta CLI login session instead of storing an API key in editor settings.

Use `cloud` for execution in an isolated cloud sandbox, `local` to keep agent state on your machine, or `remote` to connect to an [App Server](/platform/app-server/index.md) you operate.

## ACP client behavior

- **Sessions:** Each ACP session maps to a Letta conversation and can be resumed after the adapter restarts.
- **Approvals:** Tool approvals use the client’s native permission prompts. Clients that support session modes can switch between `standard`, `acceptEdits`, and `unrestricted` behavior.
- **Client files:** When the client provides filesystem capabilities, the agent can read files with `read_editor_buffer` and write through the client with `write_via_editor`. Built-in tools still run in the location shown above.
- **Slash commands:** Clients can expose supported Letta commands such as `/model`, `/compact`, `/init`, and `/remember`, along with discovered skills. Use the client UI instead of TUI-only commands such as `/resume` or `/login`.

## Configuration

| Variable                    | Effect                                                                              |
| --------------------------- | ----------------------------------------------------------------------------------- |
| `LETTA_ACP_BACKEND`         | `local` (default), `remote`, `cloud`, or `cloud-oauth`                              |
| `LETTA_AGENT_ID`            | reuse an existing agent instead of creating one                                     |
| `LETTA_ACP_MODEL`           | model override as a `provider/model` handle; run `/model` to list available handles |
| `LETTA_ACP_PERMISSION_MODE` | initial mode: `standard` (default), `acceptEdits`, or `unrestricted`                |
| `LETTA_API_KEY`             | required by `cloud`; not needed for `cloud-oauth`                                   |
| `LETTA_APP_SERVER_URL`      | `remote` backend URL; defaults to `ws://127.0.0.1:4500`                             |
| `LETTA_APP_SERVER_TOKEN`    | `remote` capability token, when authentication is enabled                           |

See the [`letta-acp` repository](https://github.com/letta-ai/letta-acp) for implementation details and release notes, or read the [App Server documentation](/platform/app-server/index.md) to build your own controller or editor integration.
