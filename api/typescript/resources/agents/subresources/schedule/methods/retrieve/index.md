## Retrieve Scheduled Agent Message

`client.agents.schedule.retrieve(stringscheduledMessageID, ScheduleRetrieveParamsparams, RequestOptionsoptions?): ScheduleRetrieveResponse`

**get** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Retrieve a scheduled message by its ID for a specific agent.

### Parameters

- `scheduledMessageID: string`

- `params: ScheduleRetrieveParams`

  - `agent_id: string`

### Returns

- `ScheduleRetrieveResponse`

  - `id: string`

  - `agent_id: string`

  - `message: Message`

    - `messages: Array<Message>`

      - `content: Array<UnionMember0 | UnionMember1> | string`

        - `Array<UnionMember0 | UnionMember1>`

          - `UnionMember0`

            - `text: string`

            - `signature?: string | null`

            - `type?: "text"`

              - `"text"`

          - `UnionMember1`

            - `source: Source`

              - `data: string`

              - `media_type: string`

              - `detail?: string`

              - `type?: "base64"`

                - `"base64"`

            - `type: "image"`

              - `"image"`

        - `string`

      - `role: "user" | "assistant" | "system"`

        - `"user"`

        - `"assistant"`

        - `"system"`

      - `name?: string`

      - `otid?: string`

      - `sender_id?: string`

      - `type?: "message"`

        - `"message"`

    - `callback_url?: string`

    - `include_return_message_types?: Array<"system_message" | "user_message" | "assistant_message" | 6 more>`

      - `"system_message"`

      - `"user_message"`

      - `"assistant_message"`

      - `"reasoning_message"`

      - `"hidden_reasoning_message"`

      - `"tool_call_message"`

      - `"tool_return_message"`

      - `"approval_request_message"`

      - `"approval_response_message"`

    - `max_steps?: number`

  - `next_scheduled_time: string | null`

  - `schedule: UnionMember0 | UnionMember1`

    - `UnionMember0`

      - `scheduled_at: number`

      - `type?: "one-time"`

        - `"one-time"`

    - `UnionMember1`

      - `cron_expression: string`

      - `type: "recurring"`

        - `"recurring"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const schedule = await client.agents.schedule.retrieve('scheduled_message_id', {
  agent_id: 'agent_id',
});

console.log(schedule.id);
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
