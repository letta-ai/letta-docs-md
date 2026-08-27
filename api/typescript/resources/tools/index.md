# Tools

## Delete Tool

`client.tools.delete(stringtoolID, RequestOptionsoptions?): ToolDeleteResponse`

**delete** `/v1/tools/{tool_id}`

Delete a tool by name

### Parameters

- `toolID: string`

  The ID of the tool in the format 'tool-<uuid4>'

### Returns

- `ToolDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const tool = await client.tools.delete('tool-123e4567-e89b-42d3-8456-426614174000');

console.log(tool);
```

#### Response

```json
{}
```

## Retrieve Tool

`client.tools.retrieve(stringtoolID, RequestOptionsoptions?): Tool`

**get** `/v1/tools/{tool_id}`

Get a tool by ID

### Parameters

- `toolID: string`

  The ID of the tool in the format 'tool-<uuid4>'

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

const tool = await client.tools.retrieve('tool-123e4567-e89b-42d3-8456-426614174000');

console.log(tool.id);
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

`client.tools.update(stringtoolID, ToolUpdateParamsbody, RequestOptionsoptions?): Tool`

**patch** `/v1/tools/{tool_id}`

Update an existing tool

### Parameters

- `toolID: string`

  The ID of the tool in the format 'tool-<uuid4>'

- `body: ToolUpdateParams`

  - `args_json_schema?: Record<string, unknown> | null`

    The args JSON schema of the function.

  - `default_requires_approval?: boolean | null`

    Whether or not to require approval before executing this tool.

  - `description?: string | null`

    The description of the tool.

  - `enable_parallel_execution?: boolean | null`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema?: Record<string, unknown> | null`

    The JSON schema of the function (auto-generated from source_code if not provided)

  - `metadata_?: Record<string, unknown> | null`

    A dictionary of additional metadata for the tool.

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

  - `return_char_limit?: number | null`

    The maximum number of characters in the response.

  - `source_code?: string | null`

    The source code of the function.

  - `source_type?: string | null`

    The type of the source code.

  - `tags?: Array<string> | null`

    Metadata tags.

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

const tool = await client.tools.update('tool-123e4567-e89b-42d3-8456-426614174000');

console.log(tool.id);
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

## Create Tool

`client.tools.create(ToolCreateParamsbody, RequestOptionsoptions?): Tool`

**post** `/v1/tools/`

Create a new tool

### Parameters

- `body: ToolCreateParams`

  - `source_code: string`

    The source code of the function.

  - `args_json_schema?: Record<string, unknown> | null`

    The args JSON schema of the function.

  - `default_requires_approval?: boolean | null`

    Whether or not to require approval before executing this tool.

  - `description?: string | null`

    The description of the tool.

  - `enable_parallel_execution?: boolean | null`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema?: Record<string, unknown> | null`

    The JSON schema of the function (auto-generated from source_code if not provided)

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

  - `return_char_limit?: number`

    The maximum number of characters in the response.

  - `source_type?: string`

    The source type of the function.

  - `tags?: Array<string> | null`

    Metadata tags.

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

const tool = await client.tools.create({ source_code: 'source_code' });

console.log(tool.id);
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

`client.tools.upsert(ToolUpsertParamsbody, RequestOptionsoptions?): Tool`

**put** `/v1/tools/`

Create or update a tool

### Parameters

- `body: ToolUpsertParams`

  - `source_code: string`

    The source code of the function.

  - `args_json_schema?: Record<string, unknown> | null`

    The args JSON schema of the function.

  - `default_requires_approval?: boolean | null`

    Whether or not to require approval before executing this tool.

  - `description?: string | null`

    The description of the tool.

  - `enable_parallel_execution?: boolean | null`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema?: Record<string, unknown> | null`

    The JSON schema of the function (auto-generated from source_code if not provided)

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

  - `return_char_limit?: number`

    The maximum number of characters in the response.

  - `source_type?: string`

    The source type of the function.

  - `tags?: Array<string> | null`

    Metadata tags.

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

const tool = await client.tools.upsert({ source_code: 'source_code' });

console.log(tool.id);
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

`client.tools.search(ToolSearchParamsbody, RequestOptionsoptions?): ToolSearchResponse`

**post** `/v1/tools/search`

Search tools using semantic search.

Requires tool embedding to be enabled (embed_tools=True). Uses vector search,
full-text search, or hybrid mode to find tools matching the query.

Returns tools ranked by relevance with their search scores.

### Parameters

- `body: ToolSearchParams`

  - `limit?: number`

    Maximum number of results to return.

  - `query?: string | null`

    Text query for semantic search.

  - `search_mode?: "vector" | "fts" | "hybrid"`

    Search mode: vector, fts, or hybrid.

    - `"vector"`

    - `"fts"`

    - `"hybrid"`

  - `tags?: Array<string> | null`

    Filter by tags (match any).

  - `tool_types?: Array<string> | null`

    Filter by tool types (e.g., 'custom', 'letta_core').

### Returns

- `ToolSearchResponse = Array<ToolSearchResult>`

  - `combined_score: number`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

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

  - `embedded_text?: string | null`

    The embedded text content used for matching.

  - `fts_rank?: number | null`

    Full-text search rank position.

  - `vector_rank?: number | null`

    Vector search rank position.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const toolSearchResults = await client.tools.search();

console.log(toolSearchResults);
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

- `NpmRequirement`

  - `name: string`

    Name of the npm package.

  - `version?: string | null`

    Optional version of the package, following semantic versioning.

### Pip Requirement

- `PipRequirement`

  - `name: string`

    Name of the pip package.

  - `version?: string | null`

    Optional version of the package, following semantic versioning.

### Tool

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

### Tool Create

- `ToolCreate`

  - `source_code: string`

    The source code of the function.

  - `args_json_schema?: Record<string, unknown> | null`

    The args JSON schema of the function.

  - `default_requires_approval?: boolean | null`

    Whether or not to require approval before executing this tool.

  - `description?: string | null`

    The description of the tool.

  - `enable_parallel_execution?: boolean | null`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema?: Record<string, unknown> | null`

    The JSON schema of the function (auto-generated from source_code if not provided)

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

  - `return_char_limit?: number`

    The maximum number of characters in the response.

  - `source_type?: string`

    The source type of the function.

  - `tags?: Array<string> | null`

    Metadata tags.

### Tool Return Message

- `ToolReturnMessage`

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

  - `status: "success" | "error"`

    - `"success"`

    - `"error"`

  - `tool_call_id: string`

  - `tool_return: string`

  - `is_err?: boolean | null`

  - `message_type?: "tool_return_message"`

    The type of the message.

    - `"tool_return_message"`

  - `name?: string | null`

  - `otid?: string | null`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id?: string | null`

  - `sender_id?: string | null`

  - `seq_id?: number | null`

  - `stderr?: Array<string> | null`

  - `stdout?: Array<string> | null`

  - `step_id?: string | null`

  - `tool_returns?: Array<ToolReturn> | null`

    - `status: "success" | "error"`

      - `"success"`

      - `"error"`

    - `tool_call_id: string`

    - `tool_return: Array<TextContent | ImageContent> | string`

      The tool return value - either a string or list of content parts (text/image)

      - `Array<TextContent | ImageContent>`

        - `TextContent`

          - `text: string`

            The text content of the message.

          - `signature?: string | null`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type?: "text"`

            The type of the message.

            - `"text"`

        - `ImageContent`

          - `source: URLImage | Base64Image | LettaImage`

            The source of the image.

            - `URLImage`

              - `url: string`

                The URL of the image.

              - `type?: "url"`

                The source type for the image.

                - `"url"`

            - `Base64Image`

              - `data: string`

                The base64 encoded image data.

              - `media_type: string`

                The media type for the image.

              - `detail?: string | null`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `type?: "base64"`

                The source type for the image.

                - `"base64"`

            - `LettaImage`

              - `file_id: string`

                The unique identifier of the image file persisted in storage.

              - `data?: string | null`

                The base64 encoded image data.

              - `detail?: string | null`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `media_type?: string | null`

                The media type for the image.

              - `type?: "letta"`

                The source type for the image.

                - `"letta"`

          - `type?: "image"`

            The type of the message.

            - `"image"`

      - `string`

    - `stderr?: Array<string> | null`

    - `stdout?: Array<string> | null`

    - `type?: "tool"`

      The message type to be created.

      - `"tool"`

### Tool Search Request

- `ToolSearchRequest`

  Request model for searching tools using semantic search.

  - `limit?: number`

    Maximum number of results to return.

  - `query?: string | null`

    Text query for semantic search.

  - `search_mode?: "vector" | "fts" | "hybrid"`

    Search mode: vector, fts, or hybrid.

    - `"vector"`

    - `"fts"`

    - `"hybrid"`

  - `tags?: Array<string> | null`

    Filter by tags (match any).

  - `tool_types?: Array<string> | null`

    Filter by tool types (e.g., 'custom', 'letta_core').

### Tool Search Result

- `ToolSearchResult`

  Result from a tool search operation.

  - `combined_score: number`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

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

  - `embedded_text?: string | null`

    The embedded text content used for matching.

  - `fts_rank?: number | null`

    Full-text search rank position.

  - `vector_rank?: number | null`

    Vector search rank position.

### Tool Type

- `ToolType = "custom" | "letta_core" | "letta_memory_core" | 8 more`

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

- `ToolSearchResponse = Array<ToolSearchResult>`

  - `combined_score: number`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

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

  - `embedded_text?: string | null`

    The embedded text content used for matching.

  - `fts_rank?: number | null`

    Full-text search rank position.

  - `vector_rank?: number | null`

    Vector search rank position.
