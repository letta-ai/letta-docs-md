## Open File For Agent

`client.agents.files.open(stringfileID, FileOpenParamsparams, RequestOptionsoptions?): FileOpenResponse`

**patch** `/v1/agents/{agent_id}/files/{file_id}/open`

Opens a specific file for a given agent.

This endpoint marks a specific file as open in the agent's file state.
The file will be included in the agent's working memory view.
Returns a list of file names that were closed due to LRU eviction.

### Parameters

- `fileID: string`

  The ID of the file in the format 'file-<uuid4>'

- `params: FileOpenParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `FileOpenResponse = Array<string>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.files.open('file-123e4567-e89b-42d3-8456-426614174000', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(response);
```

#### Response

```json
[
  "string"
]
```
