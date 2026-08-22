## Delete Passage

`agents.passages.delete(strmemory_id, PassageDeleteParams**kwargs)  -> object`

**delete** `/v1/agents/{agent_id}/archival-memory/{memory_id}`

Delete a memory from an agent's archival memory store.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `memory_id: str`

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
passage = client.agents.passages.delete(
    memory_id="memory_id",
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(passage)
```

#### Response

```json
{}
```
