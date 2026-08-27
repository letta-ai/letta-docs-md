## List Mcp Servers

`mcp_servers.list()  -> McpServerListResponse`

**get** `/v1/mcp-servers/`

Get a list of all configured MCP servers

### Returns

- `List[McpServerListResponseItem]`

  - `class StdioMcpServer: …`

    A Stdio MCP server

    - `args: List[str]`

      The arguments to pass to the command

    - `command: str`

      The command to run (MCP 'local' client will run this command)

    - `server_name: str`

      The name of the MCP server

    - `id: Optional[str]`

      The human-friendly ID of the Mcp_server

    - `env: Optional[Dict[str, str]]`

      Environment variables to set

    - `mcp_server_type: Optional[Literal["stdio"]]`

      - `"stdio"`

  - `class SseMcpServer: …`

    An SSE MCP server

    - `server_name: str`

      The name of the MCP server

    - `server_url: str`

      The URL of the server

    - `id: Optional[str]`

      The human-friendly ID of the Mcp_server

    - `auth_header: Optional[str]`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token: Optional[str]`

      The authentication token or API key value

    - `custom_headers: Optional[Dict[str, str]]`

      Custom HTTP headers to include with requests

    - `mcp_server_type: Optional[Literal["sse"]]`

      - `"sse"`

  - `class StreamableHTTPMcpServer: …`

    A Streamable HTTP MCP server

    - `server_name: str`

      The name of the MCP server

    - `server_url: str`

      The URL of the server

    - `id: Optional[str]`

      The human-friendly ID of the Mcp_server

    - `auth_header: Optional[str]`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token: Optional[str]`

      The authentication token or API key value

    - `custom_headers: Optional[Dict[str, str]]`

      Custom HTTP headers to include with requests

    - `mcp_server_type: Optional[Literal["streamable_http"]]`

      - `"streamable_http"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
mcp_servers = client.mcp_servers.list()
print(mcp_servers)
```

#### Response

```json
[
  {
    "args": [
      "string"
    ],
    "command": "command",
    "server_name": "server_name",
    "id": "mcp_server-123e4567-e89b-12d3-a456-426614174000",
    "env": {
      "foo": "string"
    },
    "mcp_server_type": "stdio"
  }
]
```
