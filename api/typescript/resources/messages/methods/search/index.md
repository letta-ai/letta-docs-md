## Search All Messages

`client.messages.search(MessageSearchParamsbody, RequestOptionsoptions?): MessageSearchResponse`

**post** `/v1/messages/search`

Search messages across the organization with optional agent filtering.
Returns messages with FTS/vector ranks and total RRF score.

This is a cloud-only feature.

### Parameters

- `body: MessageSearchParams`

  - `query: string`

    Text query for full-text search

  - `agent_id?: string | null`

    Filter messages by agent ID

  - `conversation_id?: string | null`

    Filter messages by conversation ID

  - `end_date?: string | null`

    Filter messages created on or before this date

  - `limit?: number`

    Maximum number of results to return

  - `search_mode?: "vector" | "fts" | "hybrid"`

    Search mode to use

    - `"vector"`

    - `"fts"`

    - `"hybrid"`

  - `start_date?: string | null`

    Filter messages created after this date

### Returns

- `MessageSearchResponse = Array<SystemMessageListResult | UserMessageListResult | ReasoningMessageListResult | AssistantMessageListResult>`

  - `SystemMessageListResult`

    System message list result with agent context.

    Shape is identical to UpdateSystemMessage but includes the owning agent_id and message id.

    - `content: string`

      The message content sent by the system (can be a string or an array of multi-modal content parts)

    - `created_at: string`

      The time the message was created in ISO format.

    - `message_id: string`

      The unique identifier of the message.

    - `agent_id?: string | null`

      The unique identifier of the agent that owns the message.

    - `conversation_id?: string | null`

      The unique identifier of the conversation that the message belongs to.

    - `message_type?: "system_message"`

      - `"system_message"`

  - `UserMessageListResult`

    User message list result with agent context.

    Shape is identical to UpdateUserMessage but includes the owning agent_id and message id.

    - `content: Array<LettaUserMessageContentUnion> | string`

      The message content sent by the user (can be a string or an array of multi-modal content parts)

      - `Array<LettaUserMessageContentUnion>`

        - `TextContent`

          - `text: string`

            The text content of the message.

          - `signature?: string | null`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type?: "text"`

            The type of the message.

            - `"text"`

        - `ImageContent`

          - `source: URLImage | Base64Image | LettaImage`

            The source of the image.

            - `URLImage`

              - `url: string`

                The URL of the image.

              - `type?: "url"`

                The source type for the image.

                - `"url"`

            - `Base64Image`

              - `data: string`

                The base64 encoded image data.

              - `media_type: string`

                The media type for the image.

              - `detail?: string | null`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `type?: "base64"`

                The source type for the image.

                - `"base64"`

            - `LettaImage`

              - `file_id: string`

                The unique identifier of the image file persisted in storage.

              - `data?: string | null`

                The base64 encoded image data.

              - `detail?: string | null`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `media_type?: string | null`

                The media type for the image.

              - `type?: "letta"`

                The source type for the image.

                - `"letta"`

          - `type?: "image"`

            The type of the message.

            - `"image"`

      - `string`

    - `created_at: string`

      The time the message was created in ISO format.

    - `message_id: string`

      The unique identifier of the message.

    - `agent_id?: string | null`

      The unique identifier of the agent that owns the message.

    - `conversation_id?: string | null`

      The unique identifier of the conversation that the message belongs to.

    - `message_type?: "user_message"`

      - `"user_message"`

  - `ReasoningMessageListResult`

    Reasoning message list result with agent context.

    Shape is identical to UpdateReasoningMessage but includes the owning agent_id and message id.

    - `created_at: string`

      The time the message was created in ISO format.

    - `message_id: string`

      The unique identifier of the message.

    - `reasoning: string`

    - `agent_id?: string | null`

      The unique identifier of the agent that owns the message.

    - `conversation_id?: string | null`

      The unique identifier of the conversation that the message belongs to.

    - `message_type?: "reasoning_message"`

      - `"reasoning_message"`

  - `AssistantMessageListResult`

    Assistant message list result with agent context.

    Shape is identical to UpdateAssistantMessage but includes the owning agent_id and message id.

    - `content: Array<LettaAssistantMessageContentUnion> | string`

      The message content sent by the assistant (can be a string or an array of content parts)

      - `Array<LettaAssistantMessageContentUnion>`

        - `text: string`

          The text content of the message.

        - `signature?: string | null`

          Stores a unique identifier for any reasoning associated with this text content.

        - `type?: "text"`

          The type of the message.

          - `"text"`

      - `string`

    - `created_at: string`

      The time the message was created in ISO format.

    - `message_id: string`

      The unique identifier of the message.

    - `agent_id?: string | null`

      The unique identifier of the agent that owns the message.

    - `conversation_id?: string | null`

      The unique identifier of the conversation that the message belongs to.

    - `message_type?: "assistant_message"`

      - `"assistant_message"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.messages.search({ query: 'query' });

console.log(response);
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
