---
title: Hosted Letta MCP server | Letta Docs
description: Let any MCP-capable agent create and message your stateful Letta agents
applies_to:
  backends:
    - cloud
  interfaces:
    - web
    - desktop
    - cli
    - sdk
---

Let your other agents work with your Letta agents. Any MCP client, such as Claude Code, Cursor, or another agent, can connect to `https://api.letta.com/mcp` to create stateful Letta agents, delegate work to them, and read their replies. Letta agents keep their memory across every conversation, so the calling agent does not need to resend context.

To give a Letta agent access to external MCP tools instead, see [MCP tools in the Agent SDK](/agent-sdk/mcp/index.md).

## Connect a client

Create an API key in [Letta Platform](https://platform.letta.com) and send it as a bearer token:

Cursor: .cursor/mcp.json

```
{
  "mcpServers": {
    "letta": {
      "url": "https://api.letta.com/mcp",
      "headers": { "Authorization": "Bearer <LETTA_API_KEY>" }
    }
  }
}
```

VS Code: .vscode/mcp.json

```
{
  "inputs": [
    {
      "id": "letta-api-key",
      "type": "promptString",
      "description": "Letta API key",
      "password": true
    }
  ],
  "servers": {
    "letta": {
      "type": "http",
      "url": "https://api.letta.com/mcp",
      "headers": {
        "Authorization": "Bearer ${input:letta-api-key}"
      }
    }
  }
}
```

The client must support custom bearer headers; OAuth-only clients are not supported yet.

## Tools

| Tool                 | Purpose                                             |
| -------------------- | --------------------------------------------------- |
| `list_agents`        | Find agents by name, tags, or query.                |
| `list_models`        | List models available to your project.              |
| `create_agent`       | Create a stateful agent with its own memory.        |
| `send_agent_message` | Message an agent and optionally wait for its reply. |
| `get_run`            | Check the status of a message’s run.                |
| `get_reply`          | Fetch the final reply to a sent message.            |

Full input schemas are available from `tools/list`.

## Agents and conversations

An agent keeps its memory across conversations; each conversation has its own message history. When calling `send_agent_message`:

- Pass `agent_id` to start a new conversation.
- Pass a `conv-...` `conversation_id` to continue one.
- Pass `agent_id` with `conversation_id: "default"` for the agent’s default conversation.

Messages run on a Cloud computer in unrestricted permission mode: the agent executes tools without approval prompts.

## Replies

A call waits up to 110 seconds for a reply. Longer work keeps running; use `get_reply` with the returned IDs rather than resending.

| Status               | Meaning                                                                      |
| -------------------- | ---------------------------------------------------------------------------- |
| `completed`          | The reply is included.                                                       |
| `queued`             | Accepted; the call did not wait.                                             |
| `wait_failed`        | Accepted, but waiting timed out. Call `get_reply`.                           |
| `acceptance_unknown` | The message may have been accepted. Check the conversation before resending. |
| `submission_failed`  | Not accepted.                                                                |
