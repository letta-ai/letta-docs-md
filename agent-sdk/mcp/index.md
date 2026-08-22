---
title: MCP and client tools | Letta Docs
description: Connect Letta Agent SDK sessions to stdio, HTTP, and SSE MCP servers
---

The Agent SDK can expose two kinds of tools through your Node.js process:

- **Client tools** are JavaScript functions supplied through `tools` and executed by the SDK host.
- **MCP tools** are discovered from servers supplied through `mcpServers` and proxied by the SDK host to the MCP server.

Both are scoped to the SDK session and use the same external-tool protocol. They are not persisted on the Letta agent: their implementations, processes, credentials, and filesystem access belong to the application hosting the session.

## Configure MCP servers

Pass MCP servers by name when creating or resuming a session. The SDK supports local stdio processes, Streamable HTTP, and legacy SSE:

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


await using session = client.resumeSession("agent-123", {
  mcpServers: {
    filesystem: {
      command: "npx",
      args: ["-y", "@modelcontextprotocol/server-filesystem", process.cwd()],
    },
    exa: {
      type: "http",
      url: "https://mcp.exa.ai/mcp",
    },
    github: {
      type: "http",
      url: "https://api.githubcopilot.com/mcp/",
      headers: {
        Authorization: `Bearer ${process.env.GITHUB_TOKEN}`,
      },
    },
    legacy: {
      type: "sse",
      url: "https://example.com/sse",
    },
  },
});
```

The object key becomes the server name. Discovered tools use this namespace:

```
mcp__<server>__<tool>
```

For example, Exa may expose `mcp__exa__web_search_exa` and `mcp__exa__web_fetch_exa`.

Connections start concurrently during session initialization. One unavailable server does not prevent healthy servers from connecting.

## Combine MCP and client tools

Use `tools` and `mcpServers` together when some capabilities are application functions and others come from MCP:

```
import { type AnyAgentTool, LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const lookupCustomer = {
  name: "lookup_customer",
  label: "Look up customer",
  description: "Fetch a customer record from the application database.",
  parameters: {
    type: "object",
    properties: {
      customerId: { type: "string" },
    },
    required: ["customerId"],
  },
  async execute(_toolCallId, input, signal) {
    const { customerId } = input as { customerId: string };
    const response = await fetch(
      `https://internal.example.com/customers/${customerId}`,
      { signal },
    );


    if (!response.ok) {
      return {
        isError: true,
        content: [
          {
            type: "text" as const,
            text: `Customer lookup failed: ${response.status}`,
          },
        ],
      };
    }


    const customer = await response.json();
    return {
      content: [
        {
          type: "text" as const,
          text: JSON.stringify(customer),
        },
      ],
      details: customer,
    };
  },
} satisfies AnyAgentTool;


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


await using session = client.resumeSession("agent-123", {
  tools: [lookupCustomer],
  mcpServers: {
    exa: {
      type: "http",
      url: "https://mcp.exa.ai/mcp",
    },
  },
  allowedTools: ["lookup_customer", "mcp__exa__*", "Read", "Grep"],
});


await session.send(
  "Look up customer cust_123 and research recent news about their company.",
);


for await (const message of session.stream()) {
  if (message.type === "assistant") process.stdout.write(message.content);
}
```

`allowedTools` is an availability filter in the Letta Agent SDK. If you provide it, include every client, MCP, and built-in tool the session should expose. If you omit it, registered client and MCP tools remain available alongside the harness defaults.

MCP allowlist entries support server-scoped wildcards such as `mcp__exa__*`. Client tools use their exact names.

## Authentication

Supply bearer tokens or other remote credentials through `headers`:

```
mcpServers: {
  internal: {
    type: "http",
    url: "https://mcp.example.com/mcp",
    headers: {
      Authorization: `Bearer ${process.env.MCP_ACCESS_TOKEN}`,
      "X-Organization": process.env.MCP_ORGANIZATION_ID!,
    },
  },
}
```

The Agent SDK does not open an interactive OAuth browser flow. Complete OAuth in your host application and pass the resulting access token to the session. Keep credentials in environment variables or a secret manager rather than source code.

## Execution and lifecycle

MCP connections and client tools run in the SDK’s Node.js process, including for Cloud and remote sessions. This has several consequences:

- A stdio filesystem server sees the SDK host filesystem, not a managed Cloud sandbox.
- Local executables and environment variables must exist on the SDK host.
- Different sessions on the same stateful agent may use different MCP servers and credentials.
- Closing or asynchronously disposing the session closes all of its MCP connections and child processes.

Use `await using` so asynchronous MCP shutdown completes before the surrounding scope exits:

```
await using session = client.resumeSession(agentId, {
  mcpServers,
});


await session.send("Complete the task using the configured tools.");
for await (const message of session.stream()) {
  // Handle streamed messages.
}
```

MCP requires the Node.js package entry point. It is not available from the portable `@letta-ai/letta-agent-sdk/client` entry point used by browser and React Native applications.

## What to read next

- [Permissions](/agent-sdk/permissions/index.md) — gating the tools you define here
- [Sending messages](/agent-sdk/messages/index.md) — how tool calls and results appear in the stream
- [Browser and React Native](/agent-sdk/browser/index.md) — where MCP is not available
- [SDK reference](/agent-sdk/reference/index.md) — tool and MCP option types
