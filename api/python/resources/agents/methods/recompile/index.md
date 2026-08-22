## Recompile Agent

`agents.recompile(stragent_id, AgentRecompileParams**kwargs)  -> AgentRecompileResponse`

**post** `/v1/agents/{agent_id}/recompile`

Manually trigger system prompt recompilation for an agent.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `dry_run: Optional[bool]`

  If True, do not persist changes; still returns the compiled system prompt.

- `update_timestamp: Optional[bool]`

  If True, update the in-context memory last edit timestamp embedded in the system prompt.

### Returns

- `str`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.recompile(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(response)
```

#### Response

```json
"string"
```
