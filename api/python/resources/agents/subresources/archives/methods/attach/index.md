## Attach Archive To Agent

`agents.archives.attach(strarchive_id, ArchiveAttachParams**kwargs)  -> object`

**patch** `/v1/agents/{agent_id}/archives/attach/{archive_id}`

Attach an archive to an agent.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `archive_id: str`

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.archives.attach(
    archive_id="archive_id",
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(response)
```

#### Response

```json
{}
```
