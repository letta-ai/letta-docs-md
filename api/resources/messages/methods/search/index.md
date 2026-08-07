## Search All Messages

**post** `/v1/messages/search`

Search messages across the organization with optional agent filtering.
Returns messages with FTS/vector ranks and total RRF score.

This is a cloud-only feature.

### Body Parameters

- `query: string`

  Text query for full-text search

- `agent_id: optional string`

  Filter messages by agent ID

- `conversation_id: optional string`

  Filter messages by conversation ID

- `end_date: optional string`

  Filter messages created on or before this date

- `limit: optional number`

  Maximum number of results to return

- `search_mode: optional "vector" or "fts" or "hybrid"`

  Search mode to use

  - `"vector"`

  - `"fts"`

  - `"hybrid"`

- `start_date: optional string`

  Filter messages created after this date

### Returns

- `SystemMessage object { content, created_at, message_id, 3 more }`

  System message list result with agent context.

  Shape is identical to UpdateSystemMessage but includes the owning agent_id and message id.

  - `content: string`

    The message content sent by the system (can be a string or an array of multi-modal content parts)

  - `created_at: string`

    The time the message was created in ISO format.

  - `message_id: string`

    The unique identifier of the message.

  - `agent_id: optional string`

    The unique identifier of the agent that owns the message.

  - `conversation_id: optional string`

    The unique identifier of the conversation that the message belongs to.

  - `message_type: optional "system_message"`

    - `"system_message"`

- `UserMessage object { content, created_at, message_id, 3 more }`

  User message list result with agent context.

  Shape is identical to UpdateUserMessage but includes the owning agent_id and message id.

  - `content: array of LettaUserMessageContentUnion or string`

    The message content sent by the user (can be a string or an array of multi-modal content parts)

    - `array of LettaUserMessageContentUnion`

      - `TextContent object { text, signature, type }`

        - `text: string`

          The text content of the message.

        - `signature: optional string`

          Stores a unique identifier for any reasoning associated with this text content.

        - `type: optional "text"`

          The type of the message.

          - `"text"`

      - `ImageContent object { source, type }`

        - `source: object { url, type }  or object { data, media_type, detail, type }  or object { file_id, data, detail, 2 more }`

          The source of the image.

          - `URL object { url, type }`

            - `url: string`

              The URL of the image.

            - `type: optional "url"`

              The source type for the image.

              - `"url"`

          - `Base64 object { data, media_type, detail, type }`

            - `data: string`

              The base64 encoded image data.

            - `media_type: string`

              The media type for the image.

            - `detail: optional string`

              What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

            - `type: optional "base64"`

              The source type for the image.

              - `"base64"`

          - `Letta object { file_id, data, detail, 2 more }`

            - `file_id: string`

              The unique identifier of the image file persisted in storage.

            - `data: optional string`

              The base64 encoded image data.

            - `detail: optional string`

              What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

            - `media_type: optional string`

              The media type for the image.

            - `type: optional "letta"`

              The source type for the image.

              - `"letta"`

        - `type: optional "image"`

          The type of the message.

          - `"image"`

    - `string`

  - `created_at: string`

    The time the message was created in ISO format.

  - `message_id: string`

    The unique identifier of the message.

  - `agent_id: optional string`

    The unique identifier of the agent that owns the message.

  - `conversation_id: optional string`

    The unique identifier of the conversation that the message belongs to.

  - `message_type: optional "user_message"`

    - `"user_message"`

- `ReasoningMessage object { created_at, message_id, reasoning, 3 more }`

  Reasoning message list result with agent context.

  Shape is identical to UpdateReasoningMessage but includes the owning agent_id and message id.

  - `created_at: string`

    The time the message was created in ISO format.

  - `message_id: string`

    The unique identifier of the message.

  - `reasoning: string`

  - `agent_id: optional string`

    The unique identifier of the agent that owns the message.

  - `conversation_id: optional string`

    The unique identifier of the conversation that the message belongs to.

  - `message_type: optional "reasoning_message"`

    - `"reasoning_message"`

- `AssistantMessage object { content, created_at, message_id, 3 more }`

  Assistant message list result with agent context.

  Shape is identical to UpdateAssistantMessage but includes the owning agent_id and message id.

  - `content: array of LettaAssistantMessageContentUnion or string`

    The message content sent by the assistant (can be a string or an array of content parts)

    - `array of LettaAssistantMessageContentUnion`

      - `text: string`

        The text content of the message.

      - `signature: optional string`

        Stores a unique identifier for any reasoning associated with this text content.

      - `type: optional "text"`

        The type of the message.

        - `"text"`

    - `string`

  - `created_at: string`

    The time the message was created in ISO format.

  - `message_id: string`

    The unique identifier of the message.

  - `agent_id: optional string`

    The unique identifier of the agent that owns the message.

  - `conversation_id: optional string`

    The unique identifier of the conversation that the message belongs to.

  - `message_type: optional "assistant_message"`

    - `"assistant_message"`

### Example

```http
curl https://api.letta.com/v1/messages/search \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "query": "query"
        }'
```

#### Response

```json
[
  {
    "content": "content",
    "created_at": "2019-12-27T18:11:19.117Z",
    "message_id": "message_id",
    "agent_id": "agent_id",
    "conversation_id": "conversation_id",
    "message_type": "system_message"
  }
]
```
