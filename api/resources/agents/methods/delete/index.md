## Delete Agent

**delete** `/v1/agents/{agent_id}`

Delete an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
