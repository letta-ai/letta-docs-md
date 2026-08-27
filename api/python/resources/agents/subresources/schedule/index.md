# Schedule

## Schedule Agent Message

`agents.schedule.create(stragent_id, ScheduleCreateParams**kwargs)  -> ScheduleCreateResponse`

**post** `/v1/agents/{agent_id}/schedule`

Schedule a message to be sent by the agent at a specified time or on a recurring basis.

### Parameters

- `agent_id: str`

- `messages: Iterable[Message]`

  - `content: Union[Iterable[MessageContentUnionMember0], str]`

    - `Iterable[MessageContentUnionMember0]`

      - `class MessageContentUnionMember0UnionMember0: …`

        - `text: str`

        - `signature: Optional[str]`

        - `type: Optional[Literal["text"]]`

          - `"text"`

      - `class MessageContentUnionMember0UnionMember1: …`

        - `source: MessageContentUnionMember0UnionMember1Source`

          - `data: str`

          - `media_type: str`

          - `detail: Optional[str]`

          - `type: Optional[Literal["base64"]]`

            - `"base64"`

        - `type: Literal["image"]`

          - `"image"`

    - `str`

  - `role: Literal["user", "assistant", "system"]`

    - `"user"`

    - `"assistant"`

    - `"system"`

  - `name: Optional[str]`

  - `otid: Optional[str]`

  - `sender_id: Optional[str]`

  - `type: Optional[Literal["message"]]`

    - `"message"`

- `schedule: Schedule`

  - `class ScheduleUnionMember0: …`

    - `scheduled_at: float`

    - `type: Optional[Literal["one-time"]]`

      - `"one-time"`

  - `class ScheduleUnionMember1: …`

    - `cron_expression: str`

    - `type: Literal["recurring"]`

      - `"recurring"`

- `callback_url: Optional[str]`

- `include_return_message_types: Optional[List[Literal["system_message", "user_message", "assistant_message", 6 more]]]`

  - `"system_message"`

  - `"user_message"`

  - `"assistant_message"`

  - `"reasoning_message"`

  - `"hidden_reasoning_message"`

  - `"tool_call_message"`

  - `"tool_return_message"`

  - `"approval_request_message"`

  - `"approval_response_message"`

- `max_steps: Optional[float]`

### Returns

- `class ScheduleCreateResponse: …`

  - `id: str`

  - `next_scheduled_at: Optional[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
schedule = client.agents.schedule.create(
    agent_id="agent_id",
    messages=[{
        "content": [{
            "text": "text"
        }],
        "role": "user",
    }],
    schedule={
        "scheduled_at": 0
    },
)
print(schedule.id)
```

#### Response

```json
{
  "id": "id",
  "next_scheduled_at": "next_scheduled_at"
}
```

## List Scheduled Agent Messages

`agents.schedule.list(stragent_id, ScheduleListParams**kwargs)  -> ScheduleListResponse`

**get** `/v1/agents/{agent_id}/schedule`

List all scheduled messages for a specific agent.

### Parameters

- `agent_id: str`

- `after: Optional[str]`

- `limit: Optional[str]`

### Returns

- `class ScheduleListResponse: …`

  - `has_next_page: bool`

  - `scheduled_messages: List[ScheduledMessage]`

    - `id: str`

    - `agent_id: str`

    - `message: ScheduledMessageMessage`

      - `messages: List[ScheduledMessageMessageMessage]`

        - `content: Union[List[ScheduledMessageMessageMessageContentUnionMember0], str]`

          - `List[ScheduledMessageMessageMessageContentUnionMember0]`

            - `class ScheduledMessageMessageMessageContentUnionMember0UnionMember0: …`

              - `text: str`

              - `signature: Optional[str]`

              - `type: Optional[Literal["text"]]`

                - `"text"`

            - `class ScheduledMessageMessageMessageContentUnionMember0UnionMember1: …`

              - `source: ScheduledMessageMessageMessageContentUnionMember0UnionMember1Source`

                - `data: str`

                - `media_type: str`

                - `detail: Optional[str]`

                - `type: Optional[Literal["base64"]]`

                  - `"base64"`

              - `type: Literal["image"]`

                - `"image"`

          - `str`

        - `role: Literal["user", "assistant", "system"]`

          - `"user"`

          - `"assistant"`

          - `"system"`

        - `name: Optional[str]`

        - `otid: Optional[str]`

        - `sender_id: Optional[str]`

        - `type: Optional[Literal["message"]]`

          - `"message"`

      - `callback_url: Optional[str]`

      - `include_return_message_types: Optional[List[Literal["system_message", "user_message", "assistant_message", 6 more]]]`

        - `"system_message"`

        - `"user_message"`

        - `"assistant_message"`

        - `"reasoning_message"`

        - `"hidden_reasoning_message"`

        - `"tool_call_message"`

        - `"tool_return_message"`

        - `"approval_request_message"`

        - `"approval_response_message"`

      - `max_steps: Optional[float]`

    - `next_scheduled_time: Optional[str]`

    - `schedule: ScheduledMessageSchedule`

      - `class ScheduledMessageScheduleUnionMember0: …`

        - `scheduled_at: float`

        - `type: Optional[Literal["one-time"]]`

          - `"one-time"`

      - `class ScheduledMessageScheduleUnionMember1: …`

        - `cron_expression: str`

        - `type: Literal["recurring"]`

          - `"recurring"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
schedules = client.agents.schedule.list(
    agent_id="agent_id",
)
print(schedules.has_next_page)
```

#### Response

```json
{
  "has_next_page": true,
  "scheduled_messages": [
    {
      "id": "id",
      "agent_id": "agent_id",
      "message": {
        "messages": [
          {
            "content": [
              {
                "text": "text",
                "signature": "signature",
                "type": "text"
              }
            ],
            "role": "user",
            "name": "name",
            "otid": "otid",
            "sender_id": "sender_id",
            "type": "message"
          }
        ],
        "callback_url": "https://example.com",
        "include_return_message_types": [
          "system_message"
        ],
        "max_steps": 0
      },
      "next_scheduled_time": "next_scheduled_time",
      "schedule": {
        "scheduled_at": 0,
        "type": "one-time"
      }
    }
  ]
}
```

## Retrieve Scheduled Agent Message

`agents.schedule.retrieve(strscheduled_message_id, ScheduleRetrieveParams**kwargs)  -> ScheduleRetrieveResponse`

**get** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Retrieve a scheduled message by its ID for a specific agent.

### Parameters

- `agent_id: str`

- `scheduled_message_id: str`

### Returns

- `class ScheduleRetrieveResponse: …`

  - `id: str`

  - `agent_id: str`

  - `message: Message`

    - `messages: List[MessageMessage]`

      - `content: Union[List[MessageMessageContentUnionMember0], str]`

        - `List[MessageMessageContentUnionMember0]`

          - `class MessageMessageContentUnionMember0UnionMember0: …`

            - `text: str`

            - `signature: Optional[str]`

            - `type: Optional[Literal["text"]]`

              - `"text"`

          - `class MessageMessageContentUnionMember0UnionMember1: …`

            - `source: MessageMessageContentUnionMember0UnionMember1Source`

              - `data: str`

              - `media_type: str`

              - `detail: Optional[str]`

              - `type: Optional[Literal["base64"]]`

                - `"base64"`

            - `type: Literal["image"]`

              - `"image"`

        - `str`

      - `role: Literal["user", "assistant", "system"]`

        - `"user"`

        - `"assistant"`

        - `"system"`

      - `name: Optional[str]`

      - `otid: Optional[str]`

      - `sender_id: Optional[str]`

      - `type: Optional[Literal["message"]]`

        - `"message"`

    - `callback_url: Optional[str]`

    - `include_return_message_types: Optional[List[Literal["system_message", "user_message", "assistant_message", 6 more]]]`

      - `"system_message"`

      - `"user_message"`

      - `"assistant_message"`

      - `"reasoning_message"`

      - `"hidden_reasoning_message"`

      - `"tool_call_message"`

      - `"tool_return_message"`

      - `"approval_request_message"`

      - `"approval_response_message"`

    - `max_steps: Optional[float]`

  - `next_scheduled_time: Optional[str]`

  - `schedule: Schedule`

    - `class ScheduleUnionMember0: …`

      - `scheduled_at: float`

      - `type: Optional[Literal["one-time"]]`

        - `"one-time"`

    - `class ScheduleUnionMember1: …`

      - `cron_expression: str`

      - `type: Literal["recurring"]`

        - `"recurring"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
schedule = client.agents.schedule.retrieve(
    scheduled_message_id="scheduled_message_id",
    agent_id="agent_id",
)
print(schedule.id)
```

#### Response

```json
{
  "id": "id",
  "agent_id": "agent_id",
  "message": {
    "messages": [
      {
        "content": [
          {
            "text": "text",
            "signature": "signature",
            "type": "text"
          }
        ],
        "role": "user",
        "name": "name",
        "otid": "otid",
        "sender_id": "sender_id",
        "type": "message"
      }
    ],
    "callback_url": "https://example.com",
    "include_return_message_types": [
      "system_message"
    ],
    "max_steps": 0
  },
  "next_scheduled_time": "next_scheduled_time",
  "schedule": {
    "scheduled_at": 0,
    "type": "one-time"
  }
}
```

## Delete Scheduled Agent Message

`agents.schedule.delete(strscheduled_message_id, ScheduleDeleteParams**kwargs)  -> ScheduleDeleteResponse`

**delete** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Delete a scheduled message by its ID for a specific agent.

### Parameters

- `agent_id: str`

- `scheduled_message_id: str`

### Returns

- `class ScheduleDeleteResponse: …`

  - `success: Literal[true]`

    - `true`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
schedule = client.agents.schedule.delete(
    scheduled_message_id="scheduled_message_id",
    agent_id="agent_id",
)
print(schedule.success)
```

#### Response

```json
{
  "success": true
}
```

## Domain Types

### Schedule Create Response

- `class ScheduleCreateResponse: …`

  - `id: str`

  - `next_scheduled_at: Optional[str]`

### Schedule List Response

- `class ScheduleListResponse: …`

  - `has_next_page: bool`

  - `scheduled_messages: List[ScheduledMessage]`

    - `id: str`

    - `agent_id: str`

    - `message: ScheduledMessageMessage`

      - `messages: List[ScheduledMessageMessageMessage]`

        - `content: Union[List[ScheduledMessageMessageMessageContentUnionMember0], str]`

          - `List[ScheduledMessageMessageMessageContentUnionMember0]`

            - `class ScheduledMessageMessageMessageContentUnionMember0UnionMember0: …`

              - `text: str`

              - `signature: Optional[str]`

              - `type: Optional[Literal["text"]]`

                - `"text"`

            - `class ScheduledMessageMessageMessageContentUnionMember0UnionMember1: …`

              - `source: ScheduledMessageMessageMessageContentUnionMember0UnionMember1Source`

                - `data: str`

                - `media_type: str`

                - `detail: Optional[str]`

                - `type: Optional[Literal["base64"]]`

                  - `"base64"`

              - `type: Literal["image"]`

                - `"image"`

          - `str`

        - `role: Literal["user", "assistant", "system"]`

          - `"user"`

          - `"assistant"`

          - `"system"`

        - `name: Optional[str]`

        - `otid: Optional[str]`

        - `sender_id: Optional[str]`

        - `type: Optional[Literal["message"]]`

          - `"message"`

      - `callback_url: Optional[str]`

      - `include_return_message_types: Optional[List[Literal["system_message", "user_message", "assistant_message", 6 more]]]`

        - `"system_message"`

        - `"user_message"`

        - `"assistant_message"`

        - `"reasoning_message"`

        - `"hidden_reasoning_message"`

        - `"tool_call_message"`

        - `"tool_return_message"`

        - `"approval_request_message"`

        - `"approval_response_message"`

      - `max_steps: Optional[float]`

    - `next_scheduled_time: Optional[str]`

    - `schedule: ScheduledMessageSchedule`

      - `class ScheduledMessageScheduleUnionMember0: …`

        - `scheduled_at: float`

        - `type: Optional[Literal["one-time"]]`

          - `"one-time"`

      - `class ScheduledMessageScheduleUnionMember1: …`

        - `cron_expression: str`

        - `type: Literal["recurring"]`

          - `"recurring"`

### Schedule Retrieve Response

- `class ScheduleRetrieveResponse: …`

  - `id: str`

  - `agent_id: str`

  - `message: Message`

    - `messages: List[MessageMessage]`

      - `content: Union[List[MessageMessageContentUnionMember0], str]`

        - `List[MessageMessageContentUnionMember0]`

          - `class MessageMessageContentUnionMember0UnionMember0: …`

            - `text: str`

            - `signature: Optional[str]`

            - `type: Optional[Literal["text"]]`

              - `"text"`

          - `class MessageMessageContentUnionMember0UnionMember1: …`

            - `source: MessageMessageContentUnionMember0UnionMember1Source`

              - `data: str`

              - `media_type: str`

              - `detail: Optional[str]`

              - `type: Optional[Literal["base64"]]`

                - `"base64"`

            - `type: Literal["image"]`

              - `"image"`

        - `str`

      - `role: Literal["user", "assistant", "system"]`

        - `"user"`

        - `"assistant"`

        - `"system"`

      - `name: Optional[str]`

      - `otid: Optional[str]`

      - `sender_id: Optional[str]`

      - `type: Optional[Literal["message"]]`

        - `"message"`

    - `callback_url: Optional[str]`

    - `include_return_message_types: Optional[List[Literal["system_message", "user_message", "assistant_message", 6 more]]]`

      - `"system_message"`

      - `"user_message"`

      - `"assistant_message"`

      - `"reasoning_message"`

      - `"hidden_reasoning_message"`

      - `"tool_call_message"`

      - `"tool_return_message"`

      - `"approval_request_message"`

      - `"approval_response_message"`

    - `max_steps: Optional[float]`

  - `next_scheduled_time: Optional[str]`

  - `schedule: Schedule`

    - `class ScheduleUnionMember0: …`

      - `scheduled_at: float`

      - `type: Optional[Literal["one-time"]]`

        - `"one-time"`

    - `class ScheduleUnionMember1: …`

      - `cron_expression: str`

      - `type: Literal["recurring"]`

        - `"recurring"`

### Schedule Delete Response

- `class ScheduleDeleteResponse: …`

  - `success: Literal[true]`

    - `true`
