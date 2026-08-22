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
