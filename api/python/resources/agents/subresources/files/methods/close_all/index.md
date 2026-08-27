## Close All Files For Agent

`agents.files.close_all(stragent_id)  -> FileCloseAllResponse`

**patch** `/v1/agents/{agent_id}/files/close-all`

Closes all currently open files for a given agent.

This endpoint updates the file state for the agent so that no files are marked as open.
Typically used to reset the working memory view for the agent.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `List[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.files.close_all(
    "agent-123e4567-e89b-42d3-8456-426614174000",
)
print(response)
```

#### Response

```json
[
  "string"
]
```
