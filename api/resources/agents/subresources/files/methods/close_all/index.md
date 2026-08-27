## Close All Files For Agent

**patch** `/v1/agents/{agent_id}/files/close-all`

Closes all currently open files for a given agent.

This endpoint updates the file state for the agent so that no files are marked as open.
Typically used to reset the working memory view for the agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/files/close-all \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  "string"
]
```
