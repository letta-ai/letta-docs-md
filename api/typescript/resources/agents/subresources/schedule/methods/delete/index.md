## Delete Scheduled Agent Message

`client.agents.schedule.delete(stringscheduledMessageID, ScheduleDeleteParamsparams, RequestOptionsoptions?): ScheduleDeleteResponse`

**delete** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Delete a scheduled message by its ID for a specific agent.

### Parameters

- `scheduledMessageID: string`

- `params: ScheduleDeleteParams`

  - `agent_id: string`

### Returns

- `ScheduleDeleteResponse`

  - `success: true`

    - `true`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const schedule = await client.agents.schedule.delete('scheduled_message_id', {
  agent_id: 'agent_id',
});

console.log(schedule.success);
```

#### Response

```json
{
  "success": true
}
```
