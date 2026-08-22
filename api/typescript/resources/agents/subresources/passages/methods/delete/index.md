## Delete Passage

`client.agents.passages.delete(stringmemoryID, PassageDeleteParamsparams, RequestOptionsoptions?): PassageDeleteResponse`

**delete** `/v1/agents/{agent_id}/archival-memory/{memory_id}`

Delete a memory from an agent's archival memory store.

### Parameters

- `memoryID: string`

- `params: PassageDeleteParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `PassageDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const passage = await client.agents.passages.delete('memory_id', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(passage);
```

#### Response

```json
{}
```
