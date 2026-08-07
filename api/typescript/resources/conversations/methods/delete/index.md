## Delete Conversation

`client.conversations.delete(stringconversationID, RequestOptionsoptions?): ConversationDeleteResponse`

**delete** `/v1/conversations/{conversation_id}`

Delete a conversation.

The conversation will no longer appear in list operations.

### Parameters

- `conversationID: string`

  The ID of the conv in the format 'conv-<uuid4>'

### Returns

- `ConversationDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const conversation = await client.conversations.delete('conv-123e4567-e89b-42d3-8456-426614174000');

console.log(conversation);
```

#### Response

```json
{}
```
