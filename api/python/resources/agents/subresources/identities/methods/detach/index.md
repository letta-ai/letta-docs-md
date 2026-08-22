## Detach Identity From Agent

`agents.identities.detach(stridentity_id, IdentityDetachParams**kwargs)  -> object`

**patch** `/v1/agents/{agent_id}/identities/detach/{identity_id}`

Detach an identity from an agent.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `identity_id: str`

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.identities.detach(
    identity_id="identity_id",
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(response)
```

#### Response

```json
{}
```
