## Delete Mcp Server

`client.mcpServers.delete(stringmcpServerID, RequestOptionsoptions?): void`

**delete** `/v1/mcp-servers/{mcp_server_id}`

Delete an MCP server by its ID

### Parameters

- `mcpServerID: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

await client.mcpServers.delete('mcp_server_id');
```
