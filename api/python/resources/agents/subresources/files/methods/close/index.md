## Close File For Agent

`agents.files.close(strfile_id, FileCloseParams**kwargs)  -> object`

**patch** `/v1/agents/{agent_id}/files/{file_id}/close`

Closes a specific file for a given agent.

This endpoint marks a specific file as closed in the agent's file state.
The file will be removed from the agent's working memory view.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `file_id: str`

  The ID of the file in the format 'file-<uuid4>'

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.files.close(
    file_id="file-123e4567-e89b-42d3-8456-426614174000",
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(response)
```

#### Response

```json
{}
```
