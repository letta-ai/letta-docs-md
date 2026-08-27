## Cancel Conversation

`client.conversations.cancel(stringconversationID, ConversationCancelParamsparams?, RequestOptionsoptions?): ConversationCancelResponse`

**post** `/v1/conversations/{conversation_id}/cancel`

Cancel runs associated with a conversation.

Note: To cancel active runs, Redis is required.

**Agent-direct mode**: Pass conversation_id="default" with agent_id query parameter
to cancel runs for the agent's default conversation.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Parameters

- `conversationID: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

- `params: ConversationCancelParams`

  - `agent_id?: string | null`

    Agent ID for agent-direct mode with 'default' conversation

### Returns

- `ConversationCancelResponse = Record<string, unknown>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.conversations.cancel('default');

console.log(response);
```

#### Response

```json
{
  "foo": "bar"
}
```
