## Delete Conversation

`conversations.delete(strconversation_id)  -> object`

**delete** `/v1/conversations/{conversation_id}`

Delete a conversation.

The conversation will no longer appear in list operations.

### Parameters

- `conversation_id: str`

  The ID of the conv in the format 'conv-<uuid4>'

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
conversation = client.conversations.delete(
    "conv-123e4567-e89b-42d3-8456-426614174000",
)
print(conversation)
```

#### Response

```json
{}
```
