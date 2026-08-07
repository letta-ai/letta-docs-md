## Retrieve Conversation Stream

**post** `/v1/conversations/{conversation_id}/stream`

Resume the stream for the most recent active run in a conversation.

This endpoint allows you to reconnect to an active background stream
for a conversation, enabling recovery from network interruptions.

**Agent-direct mode**: Pass conversation_id="default" with agent_id in request body
to retrieve the stream for the agent's most recent active run.

**Direct run access**: Pass run_id directly to skip run lookup entirely.
Useful for recovery from duplicate request 409 errors.

**OTID lookup**: Pass otid to look up the run_id from Redis.
Useful when you have the otid from a 409 error response.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Body Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `batch_size: optional number`

  Number of entries to read per batch.

- `include_pings: optional boolean`

  Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

- `otid: optional string`

  Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

- `poll_interval: optional number`

  Seconds to wait between polls when no new data.

- `run_id: optional string`

  Run ID to stream directly, bypassing run lookup. Use for recovery from duplicate requests.

- `starting_after: optional number`

  Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/stream \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
