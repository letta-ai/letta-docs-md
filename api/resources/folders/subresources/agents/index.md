# Agents

## List Agents For Folder

**get** `/v1/folders/{folder_id}/agents`

Get all agent IDs that have the specified folder attached.

### Path Parameters

- `folder_id: string`

  The ID of the source in the format 'source-<uuid4>'

### Query Parameters

- `after: optional string`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `before: optional string`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `limit: optional number`

  Maximum number of agents to return

- `order: optional "asc" or "desc"`

  Sort order for agents by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

### Example

```http
curl https://api.letta.com/v1/folders/$FOLDER_ID/agents \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  "string"
]
```

## Domain Types

### Agent List Response

- `AgentListResponse = array of string`
