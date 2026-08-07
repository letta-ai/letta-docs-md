## Refresh Mcp Server Tools

**patch** `/v1/mcp-servers/{mcp_server_id}/refresh`

Refresh tools for an MCP server by:

1. Fetching current tools from the MCP server
1. Deleting tools that no longer exist on the server
1. Updating schemas for existing tools
1. Adding new tools from the server

Returns a summary of changes made.

### Path Parameters

- `mcp_server_id: string`

### Query Parameters

- `agent_id: optional string`

### Example

```http
curl https://api.letta.com/v1/mcp-servers/$MCP_SERVER_ID/refresh \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
