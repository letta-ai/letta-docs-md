## Cancel Message

`agents.messages.cancel(stragent_id, MessageCancelParams**kwargs)  -> MessageCancelResponse`

**post** `/v1/agents/{agent_id}/messages/cancel`

Cancel runs associated with an agent. If run_ids are passed in, cancel those in particular.

Note to cancel active runs associated with an agent, redis is required.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `run_ids: Optional[Sequence[str]]`

  Optional list of run IDs to cancel

### Returns

- `Dict[str, object]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.messages.cancel(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(response)
```

#### Response

```json
{
  "foo": "bar"
}
```
