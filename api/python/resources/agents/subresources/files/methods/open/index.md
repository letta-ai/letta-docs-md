## Open File For Agent

`agents.files.open(strfile_id, FileOpenParams**kwargs)  -> FileOpenResponse`

**patch** `/v1/agents/{agent_id}/files/{file_id}/open`

Opens a specific file for a given agent.

This endpoint marks a specific file as open in the agent's file state.
The file will be included in the agent's working memory view.
Returns a list of file names that were closed due to LRU eviction.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `file_id: str`

  The ID of the file in the format 'file-<uuid4>'

### Returns

- `List[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.files.open(
    file_id="file-123e4567-e89b-42d3-8456-426614174000",
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(response)
```

#### Response

```json
[
  "string"
]
```
