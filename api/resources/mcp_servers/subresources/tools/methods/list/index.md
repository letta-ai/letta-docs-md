## List Tools For Mcp Server

**get** `/v1/mcp-servers/{mcp_server_id}/tools`

Get a list of all tools for a specific MCP server

### Path Parameters

- `mcp_server_id: string`

### Returns

- `id: string`

  The human-friendly ID of the Tool

- `args_json_schema: optional map[unknown]`

  The args JSON schema of the function.

- `created_by_id: optional string`

  The id of the user that made this Tool.

- `default_requires_approval: optional boolean`

  Default value for whether or not executing this tool requires approval.

- `description: optional string`

  The description of the tool.

- `enable_parallel_execution: optional boolean`

  If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

- `json_schema: optional map[unknown]`

  The JSON schema of the function.

- `last_updated_by_id: optional string`

  The id of the user that made this Tool.

- `metadata_: optional map[unknown]`

  A dictionary of additional metadata for the tool.

- `name: optional string`

  The name of the function.

- `npm_requirements: optional array of NpmRequirement`

  Optional list of npm packages required by this tool.

  - `name: string`

    Name of the npm package.

  - `version: optional string`

    Optional version of the package, following semantic versioning.

- `pip_requirements: optional array of PipRequirement`

  Optional list of pip packages required by this tool.

  - `name: string`

    Name of the pip package.

  - `version: optional string`

    Optional version of the package, following semantic versioning.

- `project_id: optional string`

  The project id of the tool.

- `return_char_limit: optional number`

  The maximum number of characters in the response.

- `source_code: optional string`

  The source code of the function.

- `source_type: optional string`

  The type of the source code.

- `tags: optional array of string`

  Metadata tags.

- `tool_type: optional ToolType`

  The type of the tool.

  - `"custom"`

  - `"letta_core"`

  - `"letta_memory_core"`

  - `"letta_multi_agent_core"`

  - `"letta_sleeptime_core"`

  - `"letta_voice_sleeptime_core"`

  - `"letta_builtin"`

  - `"letta_files_core"`

  - `"external_langchain"`

  - `"external_composio"`

  - `"external_mcp"`

### Example

```http
curl https://api.letta.com/v1/mcp-servers/$MCP_SERVER_ID/tools \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  {
    "id": "tool-123e4567-e89b-12d3-a456-426614174000",
    "args_json_schema": {
      "foo": "bar"
    },
    "created_by_id": "created_by_id",
    "default_requires_approval": true,
    "description": "description",
    "enable_parallel_execution": true,
    "json_schema": {
      "foo": "bar"
    },
    "last_updated_by_id": "last_updated_by_id",
    "metadata_": {
      "foo": "bar"
    },
    "name": "name",
    "npm_requirements": [
      {
        "name": "x",
        "version": "version"
      }
    ],
    "pip_requirements": [
      {
        "name": "x",
        "version": "version"
      }
    ],
    "project_id": "project_id",
    "return_char_limit": 1,
    "source_code": "source_code",
    "source_type": "source_type",
    "tags": [
      "string"
    ],
    "tool_type": "custom"
  }
]
```
