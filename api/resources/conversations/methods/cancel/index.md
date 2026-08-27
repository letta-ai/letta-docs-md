## Cancel Conversation

**post** `/v1/conversations/{conversation_id}/cancel`

Cancel runs associated with a conversation.

Note: To cancel active runs, Redis is required.

**Agent-direct mode**: Pass conversation_id="default" with agent_id query parameter
to cancel runs for the agent's default conversation.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Query Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/cancel \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "foo": "bar"
}
```
