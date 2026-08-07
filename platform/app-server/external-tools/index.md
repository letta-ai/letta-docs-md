---
title: External tools | Letta Docs
description: Register controller-owned tools in runtime_start and handle Letta App Server tool callbacks
---

The recommended way to interface with the App Server is the [Letta Agent SDK](/agent-sdk/index.md), which provides a high-level interface over its WebSocket protocol.

Alternatively, use the App Server’s [OpenAI-compatible API](/platform/app-server/quickstart#openai-compatible-api/index.md) with clients such as Open WebUI, or the [ACP adapter](/platform/acp/index.md) with ACP clients such as Zed.

External tools let a Letta App Server controller expose application-specific abilities to the agent without adding new built-in tools or asking the agent to shell out to a CLI.

Register external tools in `runtime_start.external_tools`. When the agent calls one, the server sends `external_tool_call_request` on the same WebSocket that registered the tool. Your controller executes the tool and responds with `external_tool_call_response`.

## When to use external tools

Use external tools for application-owned actions:

- Look up tickets, documents, CRM records, or internal resources
- Dispatch tasks to another runtime or queue
- Update a dashboard or task registry
- Call APIs that should stay inside the controller process
- Implement integration-specific commands without changing Letta Code itself

Do not use external tools for generic local computer use. Letta Code already provides local tools such as `Read`, `Grep`, `Bash`, and file editing tools.

## Register tools at runtime start

External tools are bound to the registering connection, resolved runtime, and optional scope. App Server routes callbacks only to that connection and unregisters its tools when it disconnects. This prevents tools from leaking across controllers, agents, or conversations.

runtime\_start with external tools

```
{
  "type": "runtime_start",
  "request_id": "runtime-1",
  "agent_id": "agent-123",
  "conversation_id": "conv-123",
  "external_tools": [
    {
      "tools": [
        {
          "name": "lookup_ticket",
          "label": "Lookup ticket",
          "description": "Fetch a support ticket by ID.",
          "parameters": {
            "type": "object",
            "properties": {
              "id": {
                "type": "string",
                "description": "Ticket ID, for example LET-123"
              }
            },
            "required": ["id"],
            "additionalProperties": false
          }
        }
      ]
    }
  ]
}
```

Each tool definition has:

| Field         | Required | Meaning                                            |
| ------------- | -------- | -------------------------------------------------- |
| `name`        | Yes      | Model-facing tool name                             |
| `description` | Yes      | Clear instruction for when and how to use the tool |
| `parameters`  | Yes      | JSON schema for tool input                         |
| `label`       | No       | Human-readable label for UI surfaces               |

## Handle tool calls

Use the client helper to register a callback:

external-tools.ts

```
import WebSocket from "ws";
import { createAppServerClient } from "@letta-ai/letta-code/app-server-client";


const client = await createAppServerClient({
  url: "ws://127.0.0.1:4500",
  WebSocket,
}).connect();


client.onExternalToolCall(async (request) => {
  if (request.tool_name !== "lookup_ticket") {
    throw new Error(`Unknown external tool: ${request.tool_name}`);
  }


  const id = String(request.input.id ?? "");
  const ticket = await lookupTicket(id);


  return {
    content: [
      {
        type: "text",
        text: JSON.stringify(ticket, null, 2),
      },
    ],
  };
});
```

The helper automatically sends the matching `external_tool_call_response`. If the handler throws, the helper sends an error response.

## Raw callback protocol

A raw tool call request looks like this:

external\_tool\_call\_request

```
{
  "type": "external_tool_call_request",
  "request_id": "external-tool-1",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "tool_call_id": "call-123",
  "tool_name": "lookup_ticket",
  "input": {
    "id": "LET-123"
  }
}
```

Respond on the same WebSocket with the same `request_id`:

external\_tool\_call\_response

```
{
  "type": "external_tool_call_response",
  "request_id": "external-tool-1",
  "result": {
    "content": [
      {
        "type": "text",
        "text": "Ticket LET-123 is assigned to Support."
      }
    ]
  }
}
```

For tool failures, return either a protocol error:

Protocol error

```
{
  "type": "external_tool_call_response",
  "request_id": "external-tool-1",
  "error": "Ticket system unavailable"
}
```

Or a model-visible tool result error:

Tool result error

```
{
  "type": "external_tool_call_response",
  "request_id": "external-tool-1",
  "result": {
    "is_error": true,
    "content": [
      {
        "type": "text",
        "text": "Ticket LET-123 was not found."
      }
    ]
  }
}
```

Use protocol errors for transport or controller failures. Use `is_error: true` when the tool ran successfully but the result should be interpreted as a tool-level failure.

## Scoped tools

Use `scope_id` when a tool should only be exposed on selected turns.

Scoped external tools

```
{
  "type": "runtime_start",
  "request_id": "runtime-1",
  "agent_id": "agent-123",
  "conversation_id": "conv-123",
  "external_tools": [
    {
      "tools": [
        {
          "name": "lookup_ticket",
          "description": "Fetch a support ticket by ID.",
          "parameters": {
            "type": "object",
            "properties": {
              "id": { "type": "string" }
            },
            "required": ["id"]
          }
        }
      ]
    },
    {
      "scope_id": "dispatch",
      "tools": [
        {
          "name": "dispatch_task",
          "description": "Dispatch a task to another teammate runtime.",
          "parameters": {
            "type": "object",
            "properties": {
              "target": { "type": "string" },
              "task": { "type": "string" }
            },
            "required": ["target", "task"]
          }
        }
      ]
    }
  ]
}
```

Unscoped tools are visible on ordinary turns. Scoped tools are hidden unless the turn selects their scope:

Expose scoped tools for one turn

```
{
  "type": "input",
  "runtime": {
    "agent_id": "agent-123",
    "conversation_id": "conv-123"
  },
  "payload": {
    "kind": "create_message",
    "messages": [
      {
        "role": "user",
        "content": "Split this task across the team."
      }
    ],
    "external_tool_scope_ids": ["dispatch"]
  }
}
```

Use scoped tools when a controller wants to expose powerful or context-specific abilities only for one interaction.

## Tool name isolation

App Server keys runtime-owned tools by connection, runtime identity, scope, and tool name. Different controller connections or runtimes can register the same model-facing tool name without overwriting each other’s registrations.

Within one active runtime and visible toolset, avoid duplicate model-facing names. The model sees a flat set of names after connection, runtime, and scope filtering. After reconnecting, send `runtime_start` again to restore the replacement connection’s registrations.

## Design guidance for agents

When building an App Server integration, prefer external tools over new protocol commands for product-specific behavior.

Good external tools:

- Have narrow names: `lookup_ticket`, `dispatch_task`, `mark_task_done`
- Use strict JSON schemas
- Return compact, model-readable text
- Keep durable product state in the controller database
- Include IDs the controller can correlate later

Avoid external tools that:

- Mirror every internal API endpoint one-to-one
- Return huge unfiltered payloads
- Require hidden global state not represented in the input
- Mutate important state without a clear name and schema

## Full example

tickets-controller.ts

```
import WebSocket from "ws";
import { createAppServerClient } from "@letta-ai/letta-code/app-server-client";


const client = await createAppServerClient({
  url: "ws://127.0.0.1:4500",
  WebSocket,
}).connect();


client.onExternalToolCall(async (request) => {
  switch (request.tool_name) {
    case "lookup_ticket": {
      const id = String(request.input.id ?? "");
      const ticket = await lookupTicket(id);
      return {
        content: [{ type: "text", text: JSON.stringify(ticket) }],
      };
    }
    default:
      throw new Error(`Unknown external tool: ${request.tool_name}`);
  }
});


const started = await client.runtimeStart({
  agent_id: "agent-123",
  create_conversation: { body: {} },
  external_tools: [
    {
      tools: [
        {
          name: "lookup_ticket",
          description: "Fetch a support ticket by ID.",
          parameters: {
            type: "object",
            properties: {
              id: { type: "string" },
            },
            required: ["id"],
            additionalProperties: false,
          },
        },
      ],
    },
  ],
});


if (!started.success || !started.runtime) {
  throw new Error(started.error ?? "Failed to start runtime");
}


client.input({
  runtime: started.runtime,
  payload: {
    kind: "create_message",
    messages: [
      {
        role: "user",
        content: "Look up LET-123 and summarize the next action.",
        client_message_id: "request-123",
      },
    ],
  },
});


// Keep this connection open while the turn runs. Stream events and external
// tool requests arrive through it.


async function lookupTicket(id: string) {
  return {
    id,
    title: "Customer cannot connect Slack",
    status: "open",
    priority: "high",
  };
}
```
