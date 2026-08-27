# Tools

## Delete Tool

`tools.delete(strtool_id)  -> object`

**delete** `/v1/tools/{tool_id}`

Delete a tool by name

### Parameters

- `tool_id: str`

  The ID of the tool in the format 'tool-<uuid4>'

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
tool = client.tools.delete(
    "tool-123e4567-e89b-42d3-8456-426614174000",
)
print(tool)
```

#### Response

```json
{}
```

## Retrieve Tool

`tools.retrieve(strtool_id)  -> Tool`

**get** `/v1/tools/{tool_id}`

Get a tool by ID

### Parameters

- `tool_id: str`

  The ID of the tool in the format 'tool-<uuid4>'

### Returns

- `class Tool: …`

  Representation of a tool, which is a function that can be called by the agent.

  - `id: str`

    The human-friendly ID of the Tool

  - `args_json_schema: Optional[Dict[str, object]]`

    The args JSON schema of the function.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `default_requires_approval: Optional[bool]`

    Default value for whether or not executing this tool requires approval.

  - `description: Optional[str]`

    The description of the tool.

  - `enable_parallel_execution: Optional[bool]`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: Optional[Dict[str, object]]`

    The JSON schema of the function.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    A dictionary of additional metadata for the tool.

  - `name: Optional[str]`

    The name of the function.

  - `npm_requirements: Optional[List[NpmRequirement]]`

    Optional list of npm packages required by this tool.

    - `name: str`

      Name of the npm package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: Optional[List[PipRequirement]]`

    Optional list of pip packages required by this tool.

    - `name: str`

      Name of the pip package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `project_id: Optional[str]`

    The project id of the tool.

  - `return_char_limit: Optional[int]`

    The maximum number of characters in the response.

  - `source_code: Optional[str]`

    The source code of the function.

  - `source_type: Optional[str]`

    The type of the source code.

  - `tags: Optional[List[str]]`

    Metadata tags.

  - `tool_type: Optional[ToolType]`

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

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
tool = client.tools.retrieve(
    "tool-123e4567-e89b-42d3-8456-426614174000",
)
print(tool.id)
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

`tools.update(strtool_id, ToolUpdateParams**kwargs)  -> Tool`

**patch** `/v1/tools/{tool_id}`

Update an existing tool

### Parameters

- `tool_id: str`

  The ID of the tool in the format 'tool-<uuid4>'

- `args_json_schema: Optional[Dict[str, object]]`

  The args JSON schema of the function.

- `default_requires_approval: Optional[bool]`

  Whether or not to require approval before executing this tool.

- `description: Optional[str]`

  The description of the tool.

- `enable_parallel_execution: Optional[bool]`

  If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

- `json_schema: Optional[Dict[str, object]]`

  The JSON schema of the function (auto-generated from source_code if not provided)

- `metadata: Optional[Dict[str, object]]`

  A dictionary of additional metadata for the tool.

- `npm_requirements: Optional[Iterable[NpmRequirementParam]]`

  Optional list of npm packages required by this tool.

  - `name: str`

    Name of the npm package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

- `pip_requirements: Optional[Iterable[PipRequirementParam]]`

  Optional list of pip packages required by this tool.

  - `name: str`

    Name of the pip package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

- `return_char_limit: Optional[int]`

  The maximum number of characters in the response.

- `source_code: Optional[str]`

  The source code of the function.

- `source_type: Optional[str]`

  The type of the source code.

- `tags: Optional[Sequence[str]]`

  Metadata tags.

### Returns

- `class Tool: …`

  Representation of a tool, which is a function that can be called by the agent.

  - `id: str`

    The human-friendly ID of the Tool

  - `args_json_schema: Optional[Dict[str, object]]`

    The args JSON schema of the function.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `default_requires_approval: Optional[bool]`

    Default value for whether or not executing this tool requires approval.

  - `description: Optional[str]`

    The description of the tool.

  - `enable_parallel_execution: Optional[bool]`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: Optional[Dict[str, object]]`

    The JSON schema of the function.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    A dictionary of additional metadata for the tool.

  - `name: Optional[str]`

    The name of the function.

  - `npm_requirements: Optional[List[NpmRequirement]]`

    Optional list of npm packages required by this tool.

    - `name: str`

      Name of the npm package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: Optional[List[PipRequirement]]`

    Optional list of pip packages required by this tool.

    - `name: str`

      Name of the pip package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `project_id: Optional[str]`

    The project id of the tool.

  - `return_char_limit: Optional[int]`

    The maximum number of characters in the response.

  - `source_code: Optional[str]`

    The source code of the function.

  - `source_type: Optional[str]`

    The type of the source code.

  - `tags: Optional[List[str]]`

    Metadata tags.

  - `tool_type: Optional[ToolType]`

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

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
tool = client.tools.update(
    tool_id="tool-123e4567-e89b-42d3-8456-426614174000",
)
print(tool.id)
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

`tools.list(ToolListParams**kwargs)  -> SyncArrayPage[Tool]`

**get** `/v1/tools/`

Get a list of all tools available to agents.

### Parameters

- `after: Optional[str]`

  Cursor for pagination (tool ID). Returns results relative to this ID in the specified sort order. Expected format: 'tool-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (tool ID). Returns results relative to this ID in the specified sort order. Expected format: 'tool-<uuid4>'

- `exclude_tool_types: Optional[Sequence[str]]`

  Tool type(s) to exclude - accepts repeated params or comma-separated values

- `limit: Optional[int]`

  Maximum number of tools to return

- `name: Optional[str]`

  Filter by single tool name

- `names: Optional[Sequence[str]]`

  Filter by specific tool names

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for tools by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

- `return_only_letta_tools: Optional[bool]`

  Return only tools with tool_type starting with 'letta_'

- `search: Optional[str]`

  Search tool names (case-insensitive partial match)

- `tool_ids: Optional[Sequence[str]]`

  Filter by specific tool IDs - accepts repeated params or comma-separated values

- `tool_types: Optional[Sequence[str]]`

  Filter by tool type(s) - accepts repeated params or comma-separated values

### Returns

- `class Tool: …`

  Representation of a tool, which is a function that can be called by the agent.

  - `id: str`

    The human-friendly ID of the Tool

  - `args_json_schema: Optional[Dict[str, object]]`

    The args JSON schema of the function.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `default_requires_approval: Optional[bool]`

    Default value for whether or not executing this tool requires approval.

  - `description: Optional[str]`

    The description of the tool.

  - `enable_parallel_execution: Optional[bool]`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: Optional[Dict[str, object]]`

    The JSON schema of the function.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    A dictionary of additional metadata for the tool.

  - `name: Optional[str]`

    The name of the function.

  - `npm_requirements: Optional[List[NpmRequirement]]`

    Optional list of npm packages required by this tool.

    - `name: str`

      Name of the npm package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: Optional[List[PipRequirement]]`

    Optional list of pip packages required by this tool.

    - `name: str`

      Name of the pip package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `project_id: Optional[str]`

    The project id of the tool.

  - `return_char_limit: Optional[int]`

    The maximum number of characters in the response.

  - `source_code: Optional[str]`

    The source code of the function.

  - `source_type: Optional[str]`

    The type of the source code.

  - `tags: Optional[List[str]]`

    Metadata tags.

  - `tool_type: Optional[ToolType]`

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

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.tools.list()
page = page.items[0]
print(page.id)
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

`tools.create(ToolCreateParams**kwargs)  -> Tool`

**post** `/v1/tools/`

Create a new tool

### Parameters

- `source_code: str`

  The source code of the function.

- `args_json_schema: Optional[Dict[str, object]]`

  The args JSON schema of the function.

- `default_requires_approval: Optional[bool]`

  Whether or not to require approval before executing this tool.

- `description: Optional[str]`

  The description of the tool.

- `enable_parallel_execution: Optional[bool]`

  If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

- `json_schema: Optional[Dict[str, object]]`

  The JSON schema of the function (auto-generated from source_code if not provided)

- `npm_requirements: Optional[Iterable[NpmRequirementParam]]`

  Optional list of npm packages required by this tool.

  - `name: str`

    Name of the npm package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

- `pip_requirements: Optional[Iterable[PipRequirementParam]]`

  Optional list of pip packages required by this tool.

  - `name: str`

    Name of the pip package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

- `return_char_limit: Optional[int]`

  The maximum number of characters in the response.

- `source_type: Optional[str]`

  The source type of the function.

- `tags: Optional[Sequence[str]]`

  Metadata tags.

### Returns

- `class Tool: …`

  Representation of a tool, which is a function that can be called by the agent.

  - `id: str`

    The human-friendly ID of the Tool

  - `args_json_schema: Optional[Dict[str, object]]`

    The args JSON schema of the function.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `default_requires_approval: Optional[bool]`

    Default value for whether or not executing this tool requires approval.

  - `description: Optional[str]`

    The description of the tool.

  - `enable_parallel_execution: Optional[bool]`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: Optional[Dict[str, object]]`

    The JSON schema of the function.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    A dictionary of additional metadata for the tool.

  - `name: Optional[str]`

    The name of the function.

  - `npm_requirements: Optional[List[NpmRequirement]]`

    Optional list of npm packages required by this tool.

    - `name: str`

      Name of the npm package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: Optional[List[PipRequirement]]`

    Optional list of pip packages required by this tool.

    - `name: str`

      Name of the pip package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `project_id: Optional[str]`

    The project id of the tool.

  - `return_char_limit: Optional[int]`

    The maximum number of characters in the response.

  - `source_code: Optional[str]`

    The source code of the function.

  - `source_type: Optional[str]`

    The type of the source code.

  - `tags: Optional[List[str]]`

    Metadata tags.

  - `tool_type: Optional[ToolType]`

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

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
tool = client.tools.create(
    source_code="source_code",
)
print(tool.id)
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

`tools.upsert(ToolUpsertParams**kwargs)  -> Tool`

**put** `/v1/tools/`

Create or update a tool

### Parameters

- `source_code: str`

  The source code of the function.

- `args_json_schema: Optional[Dict[str, object]]`

  The args JSON schema of the function.

- `default_requires_approval: Optional[bool]`

  Whether or not to require approval before executing this tool.

- `description: Optional[str]`

  The description of the tool.

- `enable_parallel_execution: Optional[bool]`

  If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

- `json_schema: Optional[Dict[str, object]]`

  The JSON schema of the function (auto-generated from source_code if not provided)

- `npm_requirements: Optional[Iterable[NpmRequirementParam]]`

  Optional list of npm packages required by this tool.

  - `name: str`

    Name of the npm package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

- `pip_requirements: Optional[Iterable[PipRequirementParam]]`

  Optional list of pip packages required by this tool.

  - `name: str`

    Name of the pip package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

- `return_char_limit: Optional[int]`

  The maximum number of characters in the response.

- `source_type: Optional[str]`

  The source type of the function.

- `tags: Optional[Sequence[str]]`

  Metadata tags.

### Returns

- `class Tool: …`

  Representation of a tool, which is a function that can be called by the agent.

  - `id: str`

    The human-friendly ID of the Tool

  - `args_json_schema: Optional[Dict[str, object]]`

    The args JSON schema of the function.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `default_requires_approval: Optional[bool]`

    Default value for whether or not executing this tool requires approval.

  - `description: Optional[str]`

    The description of the tool.

  - `enable_parallel_execution: Optional[bool]`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: Optional[Dict[str, object]]`

    The JSON schema of the function.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    A dictionary of additional metadata for the tool.

  - `name: Optional[str]`

    The name of the function.

  - `npm_requirements: Optional[List[NpmRequirement]]`

    Optional list of npm packages required by this tool.

    - `name: str`

      Name of the npm package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: Optional[List[PipRequirement]]`

    Optional list of pip packages required by this tool.

    - `name: str`

      Name of the pip package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `project_id: Optional[str]`

    The project id of the tool.

  - `return_char_limit: Optional[int]`

    The maximum number of characters in the response.

  - `source_code: Optional[str]`

    The source code of the function.

  - `source_type: Optional[str]`

    The type of the source code.

  - `tags: Optional[List[str]]`

    Metadata tags.

  - `tool_type: Optional[ToolType]`

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

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
tool = client.tools.upsert(
    source_code="source_code",
)
print(tool.id)
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

`tools.search(ToolSearchParams**kwargs)  -> ToolSearchResponse`

**post** `/v1/tools/search`

Search tools using semantic search.

Requires tool embedding to be enabled (embed_tools=True). Uses vector search,
full-text search, or hybrid mode to find tools matching the query.

Returns tools ranked by relevance with their search scores.

### Parameters

- `limit: Optional[int]`

  Maximum number of results to return.

- `query: Optional[str]`

  Text query for semantic search.

- `search_mode: Optional[Literal["vector", "fts", "hybrid"]]`

  Search mode: vector, fts, or hybrid.

  - `"vector"`

  - `"fts"`

  - `"hybrid"`

- `tags: Optional[Sequence[str]]`

  Filter by tags (match any).

- `tool_types: Optional[Sequence[str]]`

  Filter by tool types (e.g., 'custom', 'letta_core').

### Returns

- `List[ToolSearchResult]`

  - `combined_score: float`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

    - `id: str`

      The human-friendly ID of the Tool

    - `args_json_schema: Optional[Dict[str, object]]`

      The args JSON schema of the function.

    - `created_by_id: Optional[str]`

      The id of the user that made this Tool.

    - `default_requires_approval: Optional[bool]`

      Default value for whether or not executing this tool requires approval.

    - `description: Optional[str]`

      The description of the tool.

    - `enable_parallel_execution: Optional[bool]`

      If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

    - `json_schema: Optional[Dict[str, object]]`

      The JSON schema of the function.

    - `last_updated_by_id: Optional[str]`

      The id of the user that made this Tool.

    - `metadata: Optional[Dict[str, object]]`

      A dictionary of additional metadata for the tool.

    - `name: Optional[str]`

      The name of the function.

    - `npm_requirements: Optional[List[NpmRequirement]]`

      Optional list of npm packages required by this tool.

      - `name: str`

        Name of the npm package.

      - `version: Optional[str]`

        Optional version of the package, following semantic versioning.

    - `pip_requirements: Optional[List[PipRequirement]]`

      Optional list of pip packages required by this tool.

      - `name: str`

        Name of the pip package.

      - `version: Optional[str]`

        Optional version of the package, following semantic versioning.

    - `project_id: Optional[str]`

      The project id of the tool.

    - `return_char_limit: Optional[int]`

      The maximum number of characters in the response.

    - `source_code: Optional[str]`

      The source code of the function.

    - `source_type: Optional[str]`

      The type of the source code.

    - `tags: Optional[List[str]]`

      Metadata tags.

    - `tool_type: Optional[ToolType]`

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

  - `embedded_text: Optional[str]`

    The embedded text content used for matching.

  - `fts_rank: Optional[int]`

    Full-text search rank position.

  - `vector_rank: Optional[int]`

    Vector search rank position.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
tool_search_results = client.tools.search()
print(tool_search_results)
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

- `class NpmRequirement: …`

  - `name: str`

    Name of the npm package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

### Pip Requirement

- `class PipRequirement: …`

  - `name: str`

    Name of the pip package.

  - `version: Optional[str]`

    Optional version of the package, following semantic versioning.

### Tool

- `class Tool: …`

  Representation of a tool, which is a function that can be called by the agent.

  - `id: str`

    The human-friendly ID of the Tool

  - `args_json_schema: Optional[Dict[str, object]]`

    The args JSON schema of the function.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `default_requires_approval: Optional[bool]`

    Default value for whether or not executing this tool requires approval.

  - `description: Optional[str]`

    The description of the tool.

  - `enable_parallel_execution: Optional[bool]`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: Optional[Dict[str, object]]`

    The JSON schema of the function.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    A dictionary of additional metadata for the tool.

  - `name: Optional[str]`

    The name of the function.

  - `npm_requirements: Optional[List[NpmRequirement]]`

    Optional list of npm packages required by this tool.

    - `name: str`

      Name of the npm package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: Optional[List[PipRequirement]]`

    Optional list of pip packages required by this tool.

    - `name: str`

      Name of the pip package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `project_id: Optional[str]`

    The project id of the tool.

  - `return_char_limit: Optional[int]`

    The maximum number of characters in the response.

  - `source_code: Optional[str]`

    The source code of the function.

  - `source_type: Optional[str]`

    The type of the source code.

  - `tags: Optional[List[str]]`

    Metadata tags.

  - `tool_type: Optional[ToolType]`

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

- `class ToolCreate: …`

  - `source_code: str`

    The source code of the function.

  - `args_json_schema: Optional[Dict[str, object]]`

    The args JSON schema of the function.

  - `default_requires_approval: Optional[bool]`

    Whether or not to require approval before executing this tool.

  - `description: Optional[str]`

    The description of the tool.

  - `enable_parallel_execution: Optional[bool]`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: Optional[Dict[str, object]]`

    The JSON schema of the function (auto-generated from source_code if not provided)

  - `npm_requirements: Optional[List[NpmRequirement]]`

    Optional list of npm packages required by this tool.

    - `name: str`

      Name of the npm package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: Optional[List[PipRequirement]]`

    Optional list of pip packages required by this tool.

    - `name: str`

      Name of the pip package.

    - `version: Optional[str]`

      Optional version of the package, following semantic versioning.

  - `return_char_limit: Optional[int]`

    The maximum number of characters in the response.

  - `source_type: Optional[str]`

    The source type of the function.

  - `tags: Optional[List[str]]`

    Metadata tags.

### Tool Return Message

- `class ToolReturnMessage: …`

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

  - `id: str`

  - `date: datetime`

  - `status: Literal["success", "error"]`

    - `"success"`

    - `"error"`

  - `tool_call_id: str`

  - `tool_return: str`

  - `is_err: Optional[bool]`

  - `message_type: Optional[Literal["tool_return_message"]]`

    The type of the message.

    - `"tool_return_message"`

  - `name: Optional[str]`

  - `otid: Optional[str]`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: Optional[str]`

  - `sender_id: Optional[str]`

  - `seq_id: Optional[int]`

  - `stderr: Optional[List[str]]`

  - `stdout: Optional[List[str]]`

  - `step_id: Optional[str]`

  - `tool_returns: Optional[List[ToolReturn]]`

    - `status: Literal["success", "error"]`

      - `"success"`

      - `"error"`

    - `tool_call_id: str`

    - `tool_return: Union[List[ToolReturnUnionMember0], str]`

      The tool return value - either a string or list of content parts (text/image)

      - `List[ToolReturnUnionMember0]`

        - `class TextContent: …`

          - `text: str`

            The text content of the message.

          - `signature: Optional[str]`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type: Optional[Literal["text"]]`

            The type of the message.

            - `"text"`

        - `class ImageContent: …`

          - `source: Source`

            The source of the image.

            - `class SourceURLImage: …`

              - `url: str`

                The URL of the image.

              - `type: Optional[Literal["url"]]`

                The source type for the image.

                - `"url"`

            - `class SourceBase64Image: …`

              - `data: str`

                The base64 encoded image data.

              - `media_type: str`

                The media type for the image.

              - `detail: Optional[str]`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `type: Optional[Literal["base64"]]`

                The source type for the image.

                - `"base64"`

            - `class SourceLettaImage: …`

              - `file_id: str`

                The unique identifier of the image file persisted in storage.

              - `data: Optional[str]`

                The base64 encoded image data.

              - `detail: Optional[str]`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `media_type: Optional[str]`

                The media type for the image.

              - `type: Optional[Literal["letta"]]`

                The source type for the image.

                - `"letta"`

          - `type: Optional[Literal["image"]]`

            The type of the message.

            - `"image"`

      - `str`

    - `stderr: Optional[List[str]]`

    - `stdout: Optional[List[str]]`

    - `type: Optional[Literal["tool"]]`

      The message type to be created.

      - `"tool"`

### Tool Search Request

- `class ToolSearchRequest: …`

  Request model for searching tools using semantic search.

  - `limit: Optional[int]`

    Maximum number of results to return.

  - `query: Optional[str]`

    Text query for semantic search.

  - `search_mode: Optional[Literal["vector", "fts", "hybrid"]]`

    Search mode: vector, fts, or hybrid.

    - `"vector"`

    - `"fts"`

    - `"hybrid"`

  - `tags: Optional[List[str]]`

    Filter by tags (match any).

  - `tool_types: Optional[List[str]]`

    Filter by tool types (e.g., 'custom', 'letta_core').

### Tool Search Result

- `class ToolSearchResult: …`

  Result from a tool search operation.

  - `combined_score: float`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

    - `id: str`

      The human-friendly ID of the Tool

    - `args_json_schema: Optional[Dict[str, object]]`

      The args JSON schema of the function.

    - `created_by_id: Optional[str]`

      The id of the user that made this Tool.

    - `default_requires_approval: Optional[bool]`

      Default value for whether or not executing this tool requires approval.

    - `description: Optional[str]`

      The description of the tool.

    - `enable_parallel_execution: Optional[bool]`

      If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

    - `json_schema: Optional[Dict[str, object]]`

      The JSON schema of the function.

    - `last_updated_by_id: Optional[str]`

      The id of the user that made this Tool.

    - `metadata: Optional[Dict[str, object]]`

      A dictionary of additional metadata for the tool.

    - `name: Optional[str]`

      The name of the function.

    - `npm_requirements: Optional[List[NpmRequirement]]`

      Optional list of npm packages required by this tool.

      - `name: str`

        Name of the npm package.

      - `version: Optional[str]`

        Optional version of the package, following semantic versioning.

    - `pip_requirements: Optional[List[PipRequirement]]`

      Optional list of pip packages required by this tool.

      - `name: str`

        Name of the pip package.

      - `version: Optional[str]`

        Optional version of the package, following semantic versioning.

    - `project_id: Optional[str]`

      The project id of the tool.

    - `return_char_limit: Optional[int]`

      The maximum number of characters in the response.

    - `source_code: Optional[str]`

      The source code of the function.

    - `source_type: Optional[str]`

      The type of the source code.

    - `tags: Optional[List[str]]`

      Metadata tags.

    - `tool_type: Optional[ToolType]`

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

  - `embedded_text: Optional[str]`

    The embedded text content used for matching.

  - `fts_rank: Optional[int]`

    Full-text search rank position.

  - `vector_rank: Optional[int]`

    Vector search rank position.

### Tool Type

- `Literal["custom", "letta_core", "letta_memory_core", 8 more]`

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

### Tool Search Response

- `List[ToolSearchResult]`

  - `combined_score: float`

    Combined relevance score (RRF for hybrid mode).

  - `tool: Tool`

    The matched tool.

    - `id: str`

      The human-friendly ID of the Tool

    - `args_json_schema: Optional[Dict[str, object]]`

      The args JSON schema of the function.

    - `created_by_id: Optional[str]`

      The id of the user that made this Tool.

    - `default_requires_approval: Optional[bool]`

      Default value for whether or not executing this tool requires approval.

    - `description: Optional[str]`

      The description of the tool.

    - `enable_parallel_execution: Optional[bool]`

      If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

    - `json_schema: Optional[Dict[str, object]]`

      The JSON schema of the function.

    - `last_updated_by_id: Optional[str]`

      The id of the user that made this Tool.

    - `metadata: Optional[Dict[str, object]]`

      A dictionary of additional metadata for the tool.

    - `name: Optional[str]`

      The name of the function.

    - `npm_requirements: Optional[List[NpmRequirement]]`

      Optional list of npm packages required by this tool.

      - `name: str`

        Name of the npm package.

      - `version: Optional[str]`

        Optional version of the package, following semantic versioning.

    - `pip_requirements: Optional[List[PipRequirement]]`

      Optional list of pip packages required by this tool.

      - `name: str`

        Name of the pip package.

      - `version: Optional[str]`

        Optional version of the package, following semantic versioning.

    - `project_id: Optional[str]`

      The project id of the tool.

    - `return_char_limit: Optional[int]`

      The maximum number of characters in the response.

    - `source_code: Optional[str]`

      The source code of the function.

    - `source_type: Optional[str]`

      The type of the source code.

    - `tags: Optional[List[str]]`

      Metadata tags.

    - `tool_type: Optional[ToolType]`

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

  - `embedded_text: Optional[str]`

    The embedded text content used for matching.

  - `fts_rank: Optional[int]`

    Full-text search rank position.

  - `vector_rank: Optional[int]`

    Vector search rank position.
