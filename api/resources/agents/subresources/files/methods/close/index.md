## Close File For Agent

**patch** `/v1/agents/{agent_id}/files/{file_id}/close`

Closes a specific file for a given agent.

This endpoint marks a specific file as closed in the agent's file state.
The file will be removed from the agent's working memory view.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `file_id: string`

  The ID of the file in the format 'file-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/files/$FILE_ID/close \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
