## Import Agent

`agents.import_file(AgentImportFileParams**kwargs)  -> AgentImportFileResponse`

**post** `/v1/agents/import`

Import a serialized agent file and recreate the agent(s) in the system.
Returns the IDs of all imported agents.

### Parameters

- `file: FileTypes`

- `append_copy_suffix: Optional[bool]`

  If set to True, appends "_copy" to the end of the agent name.

- `embedding: Optional[str]`

  Embedding handle to override with.

- `env_vars_json: Optional[str]`

  Environment variables as a JSON string to pass to the agent for tool execution. Use 'secrets' instead.

- `model: Optional[str]`

  Model handle to override the agent's default model. This allows the imported agent to use a different model while keeping other defaults (e.g., context size) from the original configuration.

- `name: Optional[str]`

  If provided, overrides the agent name with this value.

- `override_embedding_handle: Optional[str]`

  Override import with specific embedding handle. Use 'embedding' instead.

- `override_existing_tools: Optional[bool]`

  If set to True, existing tools can get their source code overwritten by the uploaded tool definitions. Note that Letta core tools can never be updated externally.

- `override_model_handle: Optional[str]`

  Model handle to override the agent's default model. Use 'model' instead.

- `override_name: Optional[str]`

  If provided, overrides the agent name with this value. Use 'name' instead.

- `project_id: Optional[str]`

  The project ID to associate the uploaded agent with. This is now passed via headers.

- `secrets: Optional[str]`

  Secrets as a JSON string to pass to the agent for tool execution.

- `strip_messages: Optional[bool]`

  If set to True, strips all messages from the agent before importing.

- `x_override_embedding_model: Optional[str]`

### Returns

- `class AgentImportFileResponse: …`

  Response model for imported agents

  - `agent_ids: List[str]`

    List of IDs of the imported agents

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.import_file(
    file=b"Example data",
)
print(response.agent_ids)
```

#### Response

```json
{
  "agent_ids": [
    "string"
  ]
}
```
