## Close File For Agent

`client.agents.files.close(stringfileID, FileCloseParamsparams, RequestOptionsoptions?): FileCloseResponse`

**patch** `/v1/agents/{agent_id}/files/{file_id}/close`

Closes a specific file for a given agent.

This endpoint marks a specific file as closed in the agent's file state.
The file will be removed from the agent's working memory view.

### Parameters

- `fileID: string`

  The ID of the file in the format 'file-<uuid4>'

- `params: FileCloseParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `FileCloseResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.files.close('file-123e4567-e89b-42d3-8456-426614174000', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(response);
```

#### Response

```json
{}
```
