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
