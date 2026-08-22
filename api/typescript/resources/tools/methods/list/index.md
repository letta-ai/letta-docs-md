## List Tools

`client.tools.list(ToolListParamsquery?, RequestOptionsoptions?): ArrayPage<Tool>`

**get** `/v1/tools/`

Get a list of all tools available to agents.

### Parameters

- `query: ToolListParams`

  - `after?: string | null`

    Cursor for pagination (tool ID). Returns results relative to this ID in the specified sort order. Expected format: 'tool-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (tool ID). Returns results relative to this ID in the specified sort order. Expected format: 'tool-<uuid4>'

  - `exclude_tool_types?: Array<string> | null`

    Tool type(s) to exclude - accepts repeated params or comma-separated values

  - `limit?: number | null`

    Maximum number of tools to return

  - `name?: string | null`

    Filter by single tool name

  - `names?: Array<string> | null`

    Filter by specific tool names

  - `order?: "asc" | "desc"`

    Sort order for tools by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

  - `return_only_letta_tools?: boolean | null`

    Return only tools with tool_type starting with 'letta_'

  - `search?: string | null`

    Search tool names (case-insensitive partial match)

  - `tool_ids?: Array<string> | null`

    Filter by specific tool IDs - accepts repeated params or comma-separated values

  - `tool_types?: Array<string> | null`

    Filter by tool type(s) - accepts repeated params or comma-separated values

### Returns

- `Tool`

  Representation of a tool, which is a function that can be called by the agent.

  - `id: string`

    The human-friendly ID of the Tool

  - `args_json_schema?: Record<string, unknown> | null`

    The args JSON schema of the function.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `default_requires_approval?: boolean | null`

    Default value for whether or not executing this tool requires approval.

  - `description?: string | null`

    The description of the tool.

  - `enable_parallel_execution?: boolean | null`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema?: Record<string, unknown> | null`

    The JSON schema of the function.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata_?: Record<string, unknown> | null`

    A dictionary of additional metadata for the tool.

  - `name?: string | null`

    The name of the function.

  - `npm_requirements?: Array<NpmRequirement> | null`

    Optional list of npm packages required by this tool.

    - `name: string`

      Name of the npm package.

    - `version?: string | null`

      Optional version of the package, following semantic versioning.

  - `pip_requirements?: Array<PipRequirement> | null`

    Optional list of pip packages required by this tool.

    - `name: string`

      Name of the pip package.

    - `version?: string | null`

      Optional version of the package, following semantic versioning.

  - `project_id?: string | null`

    The project id of the tool.

  - `return_char_limit?: number`

    The maximum number of characters in the response.

  - `source_code?: string | null`

    The source code of the function.

  - `source_type?: string | null`

    The type of the source code.

  - `tags?: Array<string>`

    Metadata tags.

  - `tool_type?: ToolType`

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

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const tool of client.tools.list()) {
  console.log(tool.id);
}
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
