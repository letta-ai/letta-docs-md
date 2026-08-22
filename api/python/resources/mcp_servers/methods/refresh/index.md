## Refresh Mcp Server Tools

`mcp_servers.refresh(strmcp_server_id, McpServerRefreshParams**kwargs)  -> object`

**patch** `/v1/mcp-servers/{mcp_server_id}/refresh`

Refresh tools for an MCP server by:

1. Fetching current tools from the MCP server
1. Deleting tools that no longer exist on the server
1. Updating schemas for existing tools
1. Adding new tools from the server

Returns a summary of changes made.

### Parameters

- `mcp_server_id: str`

- `agent_id: Optional[str]`

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.mcp_servers.refresh(
    mcp_server_id="mcp_server_id",
)
print(response)
```

#### Response

```json
{}
```
