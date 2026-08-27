## Delete Scheduled Agent Message

`agents.schedule.delete(strscheduled_message_id, ScheduleDeleteParams**kwargs)  -> ScheduleDeleteResponse`

**delete** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Delete a scheduled message by its ID for a specific agent.

### Parameters

- `agent_id: str`

- `scheduled_message_id: str`

### Returns

- `class ScheduleDeleteResponse: …`

  - `success: Literal[true]`

    - `true`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
schedule = client.agents.schedule.delete(
    scheduled_message_id="scheduled_message_id",
    agent_id="agent_id",
)
print(schedule.success)
```

#### Response

```json
{
  "success": true
}
```
