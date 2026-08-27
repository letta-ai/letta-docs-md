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
