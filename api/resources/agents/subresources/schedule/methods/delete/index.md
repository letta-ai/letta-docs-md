## Delete Scheduled Agent Message

**delete** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Delete a scheduled message by its ID for a specific agent.

### Path Parameters

- `agent_id: string`

- `scheduled_message_id: string`

### Returns

- `success: true`

  - `true`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/schedule/$SCHEDULED_MESSAGE_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "success": true
}
```
