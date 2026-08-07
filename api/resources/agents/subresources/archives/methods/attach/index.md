## Attach Archive To Agent

**patch** `/v1/agents/{agent_id}/archives/attach/{archive_id}`

Attach an archive to an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `archive_id: string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archives/attach/$ARCHIVE_ID \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
