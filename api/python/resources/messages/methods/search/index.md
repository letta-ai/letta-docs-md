## Search All Messages

`messages.search(MessageSearchParams**kwargs)  -> MessageSearchResponse`

**post** `/v1/messages/search`

Search messages across the organization with optional agent filtering.
Returns messages with FTS/vector ranks and total RRF score.

This is a cloud-only feature.

### Parameters

- `query: str`

  Text query for full-text search

- `agent_id: Optional[str]`

  Filter messages by agent ID

- `conversation_id: Optional[str]`

  Filter messages by conversation ID

- `end_date: Optional[Union[str, datetime, null]]`

  Filter messages created on or before this date

- `limit: Optional[int]`

  Maximum number of results to return

- `search_mode: Optional[Literal["vector", "fts", "hybrid"]]`

  Search mode to use

  - `"vector"`

  - `"fts"`

  - `"hybrid"`

- `start_date: Optional[Union[str, datetime, null]]`

  Filter messages created after this date

### Returns

- `List[MessageSearchResponseItem]`

  - `class MessageSearchResponseItemSystemMessageListResult: …`

    System message list result with agent context.

    Shape is identical to UpdateSystemMessage but includes the owning agent_id and message id.

    - `content: str`

      The message content sent by the system (can be a string or an array of multi-modal content parts)

    - `created_at: datetime`

      The time the message was created in ISO format.

    - `message_id: str`

      The unique identifier of the message.

    - `agent_id: Optional[str]`

      The unique identifier of the agent that owns the message.

    - `conversation_id: Optional[str]`

      The unique identifier of the conversation that the message belongs to.

    - `message_type: Optional[Literal["system_message"]]`

      - `"system_message"`

  - `class MessageSearchResponseItemUserMessageListResult: …`

    User message list result with agent context.

    Shape is identical to UpdateUserMessage but includes the owning agent_id and message id.

    - `content: Union[List[LettaUserMessageContentUnion], str]`

      The message content sent by the user (can be a string or an array of multi-modal content parts)

      - `List[LettaUserMessageContentUnion]`

        - `class TextContent: …`

          - `text: str`

            The text content of the message.

          - `signature: Optional[str]`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type: Optional[Literal["text"]]`

            The type of the message.

            - `"text"`

        - `class ImageContent: …`

          - `source: Source`

            The source of the image.

            - `class SourceURLImage: …`

              - `url: str`

                The URL of the image.

              - `type: Optional[Literal["url"]]`

                The source type for the image.

                - `"url"`

            - `class SourceBase64Image: …`

              - `data: str`

                The base64 encoded image data.

              - `media_type: str`

                The media type for the image.

              - `detail: Optional[str]`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `type: Optional[Literal["base64"]]`

                The source type for the image.

                - `"base64"`

            - `class SourceLettaImage: …`

              - `file_id: str`

                The unique identifier of the image file persisted in storage.

              - `data: Optional[str]`

                The base64 encoded image data.

              - `detail: Optional[str]`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `media_type: Optional[str]`

                The media type for the image.

              - `type: Optional[Literal["letta"]]`

                The source type for the image.

                - `"letta"`

          - `type: Optional[Literal["image"]]`

            The type of the message.

            - `"image"`

      - `str`

    - `created_at: datetime`

      The time the message was created in ISO format.

    - `message_id: str`

      The unique identifier of the message.

    - `agent_id: Optional[str]`

      The unique identifier of the agent that owns the message.

    - `conversation_id: Optional[str]`

      The unique identifier of the conversation that the message belongs to.

    - `message_type: Optional[Literal["user_message"]]`

      - `"user_message"`

  - `class MessageSearchResponseItemReasoningMessageListResult: …`

    Reasoning message list result with agent context.

    Shape is identical to UpdateReasoningMessage but includes the owning agent_id and message id.

    - `created_at: datetime`

      The time the message was created in ISO format.

    - `message_id: str`

      The unique identifier of the message.

    - `reasoning: str`

    - `agent_id: Optional[str]`

      The unique identifier of the agent that owns the message.

    - `conversation_id: Optional[str]`

      The unique identifier of the conversation that the message belongs to.

    - `message_type: Optional[Literal["reasoning_message"]]`

      - `"reasoning_message"`

  - `class MessageSearchResponseItemAssistantMessageListResult: …`

    Assistant message list result with agent context.

    Shape is identical to UpdateAssistantMessage but includes the owning agent_id and message id.

    - `content: Union[List[LettaAssistantMessageContentUnion], str]`

      The message content sent by the assistant (can be a string or an array of content parts)

      - `List[LettaAssistantMessageContentUnion]`

        - `text: str`

          The text content of the message.

        - `signature: Optional[str]`

          Stores a unique identifier for any reasoning associated with this text content.

        - `type: Optional[Literal["text"]]`

          The type of the message.

          - `"text"`

      - `str`

    - `created_at: datetime`

      The time the message was created in ISO format.

    - `message_id: str`

      The unique identifier of the message.

    - `agent_id: Optional[str]`

      The unique identifier of the agent that owns the message.

    - `conversation_id: Optional[str]`

      The unique identifier of the conversation that the message belongs to.

    - `message_type: Optional[Literal["assistant_message"]]`

      - `"assistant_message"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.messages.search(
    query="query",
)
print(response)
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
