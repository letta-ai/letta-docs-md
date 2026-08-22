## Create Mcp Server

**post** `/v1/mcp-servers/`

Add a new MCP server to the Letta MCP server config

### Body Parameters

- `config: CreateStdioMcpServer or CreateSseMcpServer or CreateStreamableHTTPMcpServer`

  The MCP server configuration (Stdio, SSE, or Streamable HTTP)

  - `CreateStdioMcpServer object { args, command, env, mcp_server_type }`

    Create a new Stdio MCP server

    - `args: array of string`

      The arguments to pass to the command

    - `command: string`

      The command to run (MCP 'local' client will run this command)

    - `env: optional map[string]`

      Environment variables to set

    - `mcp_server_type: optional "stdio"`

      - `"stdio"`

  - `CreateSseMcpServer object { server_url, auth_header, auth_token, 2 more }`

    Create a new SSE MCP server

    - `server_url: string`

      The URL of the server

    - `auth_header: optional string`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token: optional string`

      The authentication token or API key value

    - `custom_headers: optional map[string]`

      Custom HTTP headers to include with requests

    - `mcp_server_type: optional "sse"`

      - `"sse"`

  - `CreateStreamableHTTPMcpServer object { server_url, auth_header, auth_token, 2 more }`

    Create a new Streamable HTTP MCP server

    - `server_url: string`

      The URL of the server

    - `auth_header: optional string`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token: optional string`

      The authentication token or API key value

    - `custom_headers: optional map[string]`

      Custom HTTP headers to include with requests

    - `mcp_server_type: optional "streamable_http"`

      - `"streamable_http"`

- `server_name: string`

  The name of the MCP server

### Returns

- `StdioMcpServer object { args, command, server_name, 3 more }`

  A Stdio MCP server

  - `args: array of string`

    The arguments to pass to the command

  - `command: string`

    The command to run (MCP 'local' client will run this command)

  - `server_name: string`

    The name of the MCP server

  - `id: optional string`

    The human-friendly ID of the Mcp_server

  - `env: optional map[string]`

    Environment variables to set

  - `mcp_server_type: optional "stdio"`

    - `"stdio"`

- `SseMcpServer object { server_name, server_url, id, 4 more }`

  An SSE MCP server

  - `server_name: string`

    The name of the MCP server

  - `server_url: string`

    The URL of the server

  - `id: optional string`

    The human-friendly ID of the Mcp_server

  - `auth_header: optional string`

    The name of the authentication header (e.g., 'Authorization')

  - `auth_token: optional string`

    The authentication token or API key value

  - `custom_headers: optional map[string]`

    Custom HTTP headers to include with requests

  - `mcp_server_type: optional "sse"`

    - `"sse"`

- `StreamableHTTPMcpServer object { server_name, server_url, id, 4 more }`

  A Streamable HTTP MCP server

  - `server_name: string`

    The name of the MCP server

  - `server_url: string`

    The URL of the server

  - `id: optional string`

    The human-friendly ID of the Mcp_server

  - `auth_header: optional string`

    The name of the authentication header (e.g., 'Authorization')

  - `auth_token: optional string`

    The authentication token or API key value

  - `custom_headers: optional map[string]`

    Custom HTTP headers to include with requests

  - `mcp_server_type: optional "streamable_http"`

    - `"streamable_http"`

### Example

```http
curl https://api.letta.com/v1/mcp-servers/ \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "config": {
            "args": [
              "string"
            ],
            "command": "command",
            "mcp_server_type": "stdio"
          },
          "server_name": "server_name"
        }'
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
