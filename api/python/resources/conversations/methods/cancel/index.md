## Cancel Conversation

`conversations.cancel(strconversation_id, ConversationCancelParams**kwargs)  -> ConversationCancelResponse`

**post** `/v1/conversations/{conversation_id}/cancel`

Cancel runs associated with a conversation.

Note: To cancel active runs, Redis is required.

**Agent-direct mode**: Pass conversation_id="default" with agent_id query parameter
to cancel runs for the agent's default conversation.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Parameters

- `conversation_id: str`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

- `agent_id: Optional[str]`

  Agent ID for agent-direct mode with 'default' conversation

### Returns

- `Dict[str, object]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.conversations.cancel(
    conversation_id="default",
)
print(response)
```

#### Response

```json
{
  "foo": "bar"
}
```
