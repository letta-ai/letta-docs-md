## Recompile Agent

**post** `/v1/agents/{agent_id}/recompile`

Manually trigger system prompt recompilation for an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Query Parameters

- `dry_run: optional boolean`

  If True, do not persist changes; still returns the compiled system prompt.

- `update_timestamp: optional boolean`

  If True, update the in-context memory last edit timestamp embedded in the system prompt.

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/recompile \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
"string"
```
