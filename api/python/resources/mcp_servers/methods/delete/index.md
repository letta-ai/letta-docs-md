## Delete Mcp Server

`mcp_servers.delete(strmcp_server_id)`

**delete** `/v1/mcp-servers/{mcp_server_id}`

Delete an MCP server by its ID

### Parameters

- `mcp_server_id: str`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
client.mcp_servers.delete(
    "mcp_server_id",
)
```
