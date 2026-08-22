## Cancel Message

`client.agents.messages.cancel(stringagentID, MessageCancelParamsbody?, RequestOptionsoptions?): MessageCancelResponse`

**post** `/v1/agents/{agent_id}/messages/cancel`

Cancel runs associated with an agent. If run_ids are passed in, cancel those in particular.

Note to cancel active runs associated with an agent, redis is required.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `body: MessageCancelParams`

  - `run_ids?: Array<string> | null`

    Optional list of run IDs to cancel

### Returns

- `MessageCancelResponse = Record<string, unknown>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.messages.cancel('agent-123e4567-e89b-42d3-8456-426614174000');

console.log(response);
```

#### Response

```json
{
  "foo": "bar"
}
```
