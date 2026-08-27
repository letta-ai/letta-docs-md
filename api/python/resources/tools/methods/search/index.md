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
