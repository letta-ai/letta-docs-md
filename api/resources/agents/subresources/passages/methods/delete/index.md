## Delete Passage

**delete** `/v1/agents/{agent_id}/archival-memory/{memory_id}`

Delete a memory from an agent's archival memory store.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `memory_id: string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archival-memory/$MEMORY_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
