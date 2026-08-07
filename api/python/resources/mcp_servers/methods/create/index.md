## Create Mcp Server

`mcp_servers.create(McpServerCreateParams**kwargs)  -> McpServerCreateResponse`

**post** `/v1/mcp-servers/`

Add a new MCP server to the Letta MCP server config

### Parameters

- `config: Config`

  The MCP server configuration (Stdio, SSE, or Streamable HTTP)

  - `class CreateStdioMcpServer: …`

    Create a new Stdio MCP server

    - `args: List[str]`

      The arguments to pass to the command

    - `command: str`

      The command to run (MCP 'local' client will run this command)

    - `env: Optional[Dict[str, str]]`

      Environment variables to set

    - `mcp_server_type: Optional[Literal["stdio"]]`

      - `"stdio"`

  - `class CreateSseMcpServer: …`

    Create a new SSE MCP server

    - `server_url: str`

      The URL of the server

    - `auth_header: Optional[str]`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token: Optional[str]`

      The authentication token or API key value

    - `custom_headers: Optional[Dict[str, str]]`

      Custom HTTP headers to include with requests

    - `mcp_server_type: Optional[Literal["sse"]]`

      - `"sse"`

  - `class CreateStreamableHTTPMcpServer: …`

    Create a new Streamable HTTP MCP server

    - `server_url: str`

      The URL of the server

    - `auth_header: Optional[str]`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token: Optional[str]`

      The authentication token or API key value

    - `custom_headers: Optional[Dict[str, str]]`

      Custom HTTP headers to include with requests

    - `mcp_server_type: Optional[Literal["streamable_http"]]`

      - `"streamable_http"`

- `server_name: str`

  The name of the MCP server

### Returns

- `McpServerCreateResponse`

  A Stdio MCP server

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
mcp_server = client.mcp_servers.create(
    config={
        "args": ["string"],
        "command": "command",
        "mcp_server_type": "stdio",
    },
    server_name="server_name",
)
print(mcp_server)
```

#### Response

```json
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
```
