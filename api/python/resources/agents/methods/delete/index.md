## Delete Agent

`agents.delete(stragent_id)  -> object`

**delete** `/v1/agents/{agent_id}`

Delete an agent.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
agent = client.agents.delete(
    "agent-123e4567-e89b-42d3-8456-426614174000",
)
print(agent)
```

#### Response

```json
{}
```
