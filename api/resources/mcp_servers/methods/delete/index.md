## Delete Mcp Server

**delete** `/v1/mcp-servers/{mcp_server_id}`

Delete an MCP server by its ID

### Path Parameters

- `mcp_server_id: string`

### Example

```http
curl https://api.letta.com/v1/mcp-servers/$MCP_SERVER_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```
