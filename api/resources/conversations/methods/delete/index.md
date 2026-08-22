## Delete Conversation

**delete** `/v1/conversations/{conversation_id}`

Delete a conversation.

The conversation will no longer appear in list operations.

### Path Parameters

- `conversation_id: string`

  The ID of the conv in the format 'conv-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
