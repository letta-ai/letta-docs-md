## Close All Files For Agent

`client.agents.files.closeAll(stringagentID, RequestOptionsoptions?): FileCloseAllResponse`

**patch** `/v1/agents/{agent_id}/files/close-all`

Closes all currently open files for a given agent.

This endpoint updates the file state for the agent so that no files are marked as open.
Typically used to reset the working memory view for the agent.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `FileCloseAllResponse = Array<string>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.files.closeAll('agent-123e4567-e89b-42d3-8456-426614174000');

console.log(response);
```

#### Response

```json
[
  "string"
]
```
