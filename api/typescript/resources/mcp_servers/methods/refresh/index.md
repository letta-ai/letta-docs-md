## Refresh Mcp Server Tools

`client.mcpServers.refresh(stringmcpServerID, McpServerRefreshParamsparams?, RequestOptionsoptions?): McpServerRefreshResponse`

**patch** `/v1/mcp-servers/{mcp_server_id}/refresh`

Refresh tools for an MCP server by:

1. Fetching current tools from the MCP server
1. Deleting tools that no longer exist on the server
1. Updating schemas for existing tools
1. Adding new tools from the server

Returns a summary of changes made.

### Parameters

- `mcpServerID: string`

- `params: McpServerRefreshParams`

  - `agent_id?: string | null`

### Returns

- `McpServerRefreshResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.mcpServers.refresh('mcp_server_id');

console.log(response);
```

#### Response

```json
{}
```
