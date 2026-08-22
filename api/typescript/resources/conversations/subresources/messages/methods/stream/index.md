## Retrieve Conversation Stream

`client.conversations.messages.stream(stringconversationID, MessageStreamParamsbody?, RequestOptionsoptions?): MessageStreamResponse | Stream<LettaStreamingResponse>`

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

### Parameters

- `conversationID: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

- `body: MessageStreamParams`

  - `agent_id?: string | null`

    Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

  - `batch_size?: number | null`

    Number of entries to read per batch.

  - `include_pings?: boolean | null`

    Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

  - `otid?: string | null`

    Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

  - `poll_interval?: number | null`

    Seconds to wait between polls when no new data.

  - `run_id?: string | null`

    Run ID to stream directly, bypassing run lookup. Use for recovery from duplicate requests.

  - `starting_after?: number`

    Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Returns

- `MessageStreamResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.conversations.messages.stream('default');

console.log(response);
```

#### Response

```json
{}
```
