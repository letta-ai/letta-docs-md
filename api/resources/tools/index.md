# Tools

## Delete Tool

**delete** `/v1/tools/{tool_id}`

Delete a tool by name

### Path Parameters

- `tool_id: string`

  The ID of the tool in the format 'tool-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/tools/$TOOL_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## Retrieve Tool

**get** `/v1/tools/{tool_id}`

Get a tool by ID

### Path Parameters

- `tool_id: string`

  The ID of the tool in the format 'tool-<uuid4>'

### Returns

- `Tool object { id, args_json_schema, created_by_id, 15 more }`

  Representation of a tool, which is a function that can be called by the agent.

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
curl https://api.letta.com/v1/tools/$TOOL_ID \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
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
```

## Update Tool

**patch** `/v1/tools/{tool_id}`

Update an existing tool

### Path Parameters

- `tool_id: string`

  The ID of the tool in the format 'tool-<uuid4>'

### Body Parameters

- `args_json_schema: optional map[unknown]`

  The args JSON schema of the function.

- `default_requires_approval: optional boolean`

  Whether or not to require approval before executing this tool.

- `description: optional string`

  The description of the tool.

- `enable_parallel_execution: optional boolean`

  If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

- `json_schema: optional map[unknown]`

  The JSON schema of the function (auto-generated from source_code if not provided)

- `metadata_: optional map[unknown]`

  A dictionary of additional metadata for the tool.

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

- `return_char_limit: optional number`

  The maximum number of characters in the response.

- `source_code: optional string`

  The source code of the function.

- `source_type: optional string`

  The type of the source code.

- `tags: optional array of string`

  Metadata tags.

### Returns

- `Tool object { id, args_json_schema, created_by_id, 15 more }`

  Representation of a tool, which is a function that can be called by the agent.

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
curl https://api.letta.com/v1/tools/$TOOL_ID \
    -X PATCH \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
```

#### Response

```json
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
```

## List Tools

**get** `/v1/tools/`

Get a list of all tools available to agents.

### Query Parameters

- `after: optional string`

  Cursor for pagination (tool ID). Returns results relative to this ID in the specified sort order. Expected format: 'tool-<uuid4>'

- `before: optional string`

  Cursor for pagination (tool ID). Returns results relative to this ID in the specified sort order. Expected format: 'tool-<uuid4>'

- `exclude_tool_types: optional array of string`

  Tool type(s) to exclude - accepts repeated params or comma-separated values

- `limit: optional number`

  Maximum number of tools to return

- `name: optional string`

  Filter by single tool name

- `names: optional array of string`

  Filter by specific tool names

- `order: optional "asc" or "desc"`

  Sort order for tools by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

- `return_only_letta_tools: optional boolean`

  Return only tools with tool_type starting with 'letta_'

- `search: optional string`

  Search tool names (case-insensitive partial match)

- `tool_ids: optional array of string`

  Filter by specific tool IDs - accepts repeated params or comma-separated values

- `tool_types: optional array of string`

  Filter by tool type(s) - accepts repeated params or comma-separated values

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
curl https://api.letta.com/v1/tools/ \
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

## Create Tool

**post** `/v1/tools/`

Create a new tool

### Body Parameters

- `source_code: string`

  The source code of the function.

- `args_json_schema: optional map[unknown]`

  The args JSON schema of the function.

- `default_requires_approval: optional boolean`

  Whether or not to require approval before executing this tool.

- `description: optional string`

  The description of the tool.

- `enable_parallel_execution: optional boolean`

  If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

- `json_schema: optional map[unknown]`

  The JSON schema of the function (auto-generated from source_code if not provided)

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

- `return_char_limit: optional number`

  The maximum number of characters in the response.

- `source_type: optional string`

  The source type of the function.

- `tags: optional array of string`

  Metadata tags.

### Returns

- `Tool object { id, args_json_schema, created_by_id, 15 more }`

  Representation of a tool, which is a function that can be called by the agent.

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
curl https://api.letta.com/v1/tools/ \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "source_code": "source_code"
        }'
```

#### Response

```json
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
```

## Upsert Tool

**put** `/v1/tools/`

Create or update a tool

### Body Parameters

- `source_code: string`

  The source code of the function.

- `args_json_schema: optional map[unknown]`

  The args JSON schema of the function.

- `default_requires_approval: optional boolean`

  Whether or not to require approval before executing this tool.

- `description: optional string`

  The description of the tool.

- `enable_parallel_execution: optional boolean`

  If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

- `json_schema: optional map[unknown]`

  The JSON schema of the function (auto-generated from source_code if not provided)

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

- `return_char_limit: optional number`

  The maximum number of characters in the response.

- `source_type: optional string`

  The source type of the function.

- `tags: optional array of string`

  Metadata tags.

### Returns

- `Tool object { id, args_json_schema, created_by_id, 15 more }`

  Representation of a tool, which is a function that can be called by the agent.

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
curl https://api.letta.com/v1/tools/ \
    -X PUT \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "source_code": "source_code"
        }'
```

#### Response

```json
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
```

## Search Tools

**post** `/v1/tools/search`

Search tools using semantic search.

Requires tool embedding to be enabled (embed_tools=True). Uses vector search,
full-text search, or hybrid mode to find tools matching the query.

Returns tools ranked by relevance with their search scores.

### Body Parameters

- `limit: optional number`

  Maximum number of results to return.

- `query: optional string`

  Text query for semantic search.

- `search_mode: optional "vector" or "fts" or "hybrid"`

  Search mode: vector, fts, or hybrid.

  - `"vector"`

  - `"fts"`

  - `"hybrid"`

- `tags: optional array of string`

  Filter by tags (match any).

- `tool_types: optional array of string`

  Filter by tool types (e.g., 'custom', 'letta_core').

### Returns

- `combined_score: number`

  Combined relevance score (RRF for hybrid mode).

- `tool: Tool`

  The matched tool.

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

- `embedded_text: optional string`

  The embedded text content used for matching.

- `fts_rank: optional number`

  Full-text search rank position.

- `vector_rank: optional number`

  Vector search rank position.

### Example

```http
curl https://api.letta.com/v1/tools/search \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
```

#### Response

```json
[
  {
    "combined_score": 0,
    "tool": {
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
    },
    "embedded_text": "embedded_text",
    "fts_rank": 0,
    "vector_rank": 0
  }
]
```

## Domain Types

### Npm Requirement

- `NpmRequirement object { name, version }`

  - `name: string`

    Name of the npm package.

  - `version: optional string`

    Optional version of the package, following semantic versioning.

### Pip Requirement

- `PipRequirement object { name, version }`

  - `name: string`

    Name of the pip package.

  - `version: optional string`

    Optional version of the package, following semantic versioning.

### Tool

- `Tool object { id, args_json_schema, created_by_id, 15 more }`

  Representation of a tool, which is a function that can be called by the agent.

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

### Tool Create

- `ToolCreate object { source_code, args_json_schema, default_requires_approval, 8 more }`

  - `source_code: string`

    The source code of the function.

  - `args_json_schema: optional map[unknown]`

    The args JSON schema of the function.

  - `default_requires_approval: optional boolean`

    Whether or not to require approval before executing this tool.

  - `description: optional string`

    The description of the tool.

  - `enable_parallel_execution: optional boolean`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: optional map[unknown]`

    The JSON schema of the function (auto-generated from source_code if not provided)

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

  - `return_char_limit: optional number`

    The maximum number of characters in the response.

  - `source_type: optional string`

    The source type of the function.

  - `tags: optional array of string`

    Metadata tags.

### Tool Return Message

- `ToolReturnMessage object { id, date, status, 13 more }`

  A message representing the return value of a tool call (generated by Letta executing the requested tool).

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  tool_return (str): The return value of the tool (deprecated, use tool_returns)
  status (Literal["success", "error"]): The status of the tool call (deprecated, use tool_returns)
  tool_call_id (str): A unique identifier for the tool call that generated this message (deprecated, use tool_returns)
  stdout (Optional[List(str)]): Captured stdout (e.g. prints, logs) from the tool invocation (deprecated, use tool_returns)
  stderr (Optional[List(str)]): Captured stderr from the tool invocation (deprecated, use tool_returns)
  tool_returns (Optional[List[ToolReturn]]): List of tool returns for multi-tool support

  - `id: string`

  - `date: string`

  - `status: "success" or "error"`

    - `"success"`

    - `"error"`

  - `tool_call_id: string`

  - `tool_return: string`

  - `is_err: optional boolean`

  - `message_type: optional "tool_return_message"`

    The type of the message.

    - `"tool_return_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `stderr: optional array of string`

  - `stdout: optional array of string`

  - `step_id: optional string`

  - `tool_returns: optional array of ToolReturn`

    - `status: "success" or "error"`

      - `"success"`

      - `"error"`

    - `tool_call_id: string`

    - `tool_return: array of TextContent or ImageContent or string`

      The tool return value - either a string or list of content parts (text/image)

      - `array of TextContent or ImageContent`

        - `TextContent object { text, signature, type }`

          - `text: string`

            The text content of the message.

          - `signature: optional string`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type: optional "text"`

            The type of the message.

            - `"text"`

        - `ImageContent object { source, type }`

          - `source: object { url, type }  or object { data, media_type, detail, type }  or object { file_id, data, detail, 2 more }`

            The source of the image.

            - `URL object { url, type }`

              - `url: string`

                The URL of the image.

              - `type: optional "url"`

                The source type for the image.

                - `"url"`

            - `Base64 object { data, media_type, detail, type }`

              - `data: string`

                The base64 encoded image data.

              - `media_type: string`

                The media type for the image.

              - `detail: optional string`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `type: optional "base64"`

                The source type for the image.

                - `"base64"`

            - `Letta object { file_id, data, detail, 2 more }`

              - `file_id: string`

                The unique identifier of the image file persisted in storage.

              - `data: optional string`

                The base64 encoded image data.

              - `detail: optional string`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `media_type: optional string`

                The media type for the image.

              - `type: optional "letta"`

                The source type for the image.

                - `"letta"`

          - `type: optional "image"`

            The type of the message.

            - `"image"`

      - `string`

    - `stderr: optional array of string`

    - `stdout: optional array of string`

    - `type: optional "tool"`

      The message type to be created.

      - `"tool"`

### Tool Search Request

- `ToolSearchRequest object { limit, query, search_mode, 2 more }`

  Request model for searching tools using semantic search.

  - `limit: optional number`

    Maximum number of results to return.

  - `query: optional string`

    Text query for semantic search.

  - `search_mode: optional "vector" or "fts" or "hybrid"`

    Search mode: vector, fts, or hybrid.

    - `"vector"`

    - `"fts"`

    - `"hybrid"`

  - `tags: optional array of string`

    Filter by tags (match any).

  - `tool_types: optional array of string`

    Filter by tool types (e.g., 'custom', 'letta_core').

### Tool Search Result

- `ToolSearchResult object { combined_score, tool, embedded_text, 2 more }`

  Result from a tool search operation.

  - `combined_score: number`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

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

  - `embedded_text: optional string`

    The embedded text content used for matching.

  - `fts_rank: optional number`

    Full-text search rank position.

  - `vector_rank: optional number`

    Vector search rank position.

### Tool Type

- `ToolType = "custom" or "letta_core" or "letta_memory_core" or 8 more`

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

### Tool Delete Response

- `ToolDeleteResponse = unknown`

### Tool Search Response

- `ToolSearchResponse = array of ToolSearchResult`

  - `combined_score: number`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

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

  - `embedded_text: optional string`

    The embedded text content used for matching.

  - `fts_rank: optional number`

    Full-text search rank position.

  - `vector_rank: optional number`

    Vector search rank position.
