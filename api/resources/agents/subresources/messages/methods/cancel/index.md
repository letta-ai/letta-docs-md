## Cancel Message

**post** `/v1/agents/{agent_id}/messages/cancel`

Cancel runs associated with an agent. If run_ids are passed in, cancel those in particular.

Note to cancel active runs associated with an agent, redis is required.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Body Parameters

- `run_ids: optional array of string`

  Optional list of run IDs to cancel

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/messages/cancel \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "foo": "bar"
}
```
