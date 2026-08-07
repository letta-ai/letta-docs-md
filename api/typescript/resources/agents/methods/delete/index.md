## Delete Agent

`client.agents.delete(stringagentID, RequestOptionsoptions?): AgentDeleteResponse`

**delete** `/v1/agents/{agent_id}`

Delete an agent.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `AgentDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const agent = await client.agents.delete('agent-123e4567-e89b-42d3-8456-426614174000');

console.log(agent);
```

#### Response

```json
{}
```
