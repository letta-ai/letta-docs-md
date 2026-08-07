## List Mcp Servers

`client.mcpServers.list(RequestOptionsoptions?): McpServerListResponse`

**get** `/v1/mcp-servers/`

Get a list of all configured MCP servers

### Returns

- `McpServerListResponse = Array<StdioMcpServer | SseMcpServer | StreamableHTTPMcpServer>`

  - `StdioMcpServer`

    A Stdio MCP server

    - `args: Array<string>`

      The arguments to pass to the command

    - `command: string`

      The command to run (MCP 'local' client will run this command)

    - `server_name: string`

      The name of the MCP server

    - `id?: string`

      The human-friendly ID of the Mcp_server

    - `env?: Record<string, string> | null`

      Environment variables to set

    - `mcp_server_type?: "stdio"`

      - `"stdio"`

  - `SseMcpServer`

    An SSE MCP server

    - `server_name: string`

      The name of the MCP server

    - `server_url: string`

      The URL of the server

    - `id?: string`

      The human-friendly ID of the Mcp_server

    - `auth_header?: string | null`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token?: string | null`

      The authentication token or API key value

    - `custom_headers?: Record<string, string> | null`

      Custom HTTP headers to include with requests

    - `mcp_server_type?: "sse"`

      - `"sse"`

  - `StreamableHTTPMcpServer`

    A Streamable HTTP MCP server

    - `server_name: string`

      The name of the MCP server

    - `server_url: string`

      The URL of the server

    - `id?: string`

      The human-friendly ID of the Mcp_server

    - `auth_header?: string | null`

      The name of the authentication header (e.g., 'Authorization')

    - `auth_token?: string | null`

      The authentication token or API key value

    - `custom_headers?: Record<string, string> | null`

      Custom HTTP headers to include with requests

    - `mcp_server_type?: "streamable_http"`

      - `"streamable_http"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const mcpServers = await client.mcpServers.list();

console.log(mcpServers);
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
