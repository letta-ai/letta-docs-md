## Export Agent

`agents.export_file(stragent_id, AgentExportFileParams**kwargs)  -> AgentExportFileResponse`

**get** `/v1/agents/{agent_id}/export`

Export the serialized JSON representation of an agent, formatted with indentation.

### Parameters

- `agent_id: str`

- `conversation_id: Optional[str]`

  Conversation ID to export. If provided, uses messages from this conversation instead of the agent's global message history.

- `max_steps: Optional[int]`

- `scrub_messages: Optional[bool]`

  If True, excludes all messages from the export. Useful for sharing agent configs without conversation history.

- `use_legacy_format: Optional[bool]`

  If True, exports using the legacy single-agent 'v1' format with inline tools/blocks. If False, exports using the new multi-entity 'v2' format, with separate agents, tools, blocks, files, etc.

### Returns

- `str`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.export_file(
    agent_id="agent_id",
)
print(response)
```

#### Response

```json
"string"
```
