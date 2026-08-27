## Attach Archive To Agent

`client.agents.archives.attach(stringarchiveID, ArchiveAttachParamsparams, RequestOptionsoptions?): ArchiveAttachResponse`

**patch** `/v1/agents/{agent_id}/archives/attach/{archive_id}`

Attach an archive to an agent.

### Parameters

- `archiveID: string`

- `params: ArchiveAttachParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `ArchiveAttachResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.archives.attach('archive_id', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(response);
```

#### Response

```json
{}
```
