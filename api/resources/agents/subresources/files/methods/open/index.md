## Open File For Agent

**patch** `/v1/agents/{agent_id}/files/{file_id}/open`

Opens a specific file for a given agent.

This endpoint marks a specific file as open in the agent's file state.
The file will be included in the agent's working memory view.
Returns a list of file names that were closed due to LRU eviction.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `file_id: string`

  The ID of the file in the format 'file-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/files/$FILE_ID/open \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  "string"
]
```
