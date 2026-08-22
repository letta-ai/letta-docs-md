## List Agents For Folder

`folders.agents.list(strfolder_id, AgentListParams**kwargs)  -> AgentListResponse`

**get** `/v1/folders/{folder_id}/agents`

Get all agent IDs that have the specified folder attached.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `after: Optional[str]`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `limit: Optional[int]`

  Maximum number of agents to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for agents by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `List[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
agents = client.folders.agents.list(
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
print(agents)
```

#### Response

```json
[
  "string"
]
```
