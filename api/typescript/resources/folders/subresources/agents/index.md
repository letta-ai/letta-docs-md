# Agents

## List Agents For Folder

`client.folders.agents.list(stringfolderID, AgentListParamsquery?, RequestOptionsoptions?): AgentListResponse`

**get** `/v1/folders/{folder_id}/agents`

Get all agent IDs that have the specified folder attached.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `query: AgentListParams`

  - `after?: string | null`

    Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

  - `limit?: number | null`

    Maximum number of agents to return

  - `order?: "asc" | "desc"`

    Sort order for agents by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `AgentListResponse = Array<string>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const agents = await client.folders.agents.list('source-123e4567-e89b-42d3-8456-426614174000');

console.log(agents);
```

#### Response

```json
[
  "string"
]
```

## Domain Types

### Agent List Response

- `AgentListResponse = Array<string>`
