## Schedule Agent Message

`client.agents.schedule.create(stringagentID, ScheduleCreateParamsbody, RequestOptionsoptions?): ScheduleCreateResponse`

**post** `/v1/agents/{agent_id}/schedule`

Schedule a message to be sent by the agent at a specified time or on a recurring basis.

### Parameters

- `agentID: string`

- `body: ScheduleCreateParams`

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

  - `schedule: UnionMember0 | UnionMember1`

    - `UnionMember0`

      - `scheduled_at: number`

      - `type?: "one-time"`

        - `"one-time"`

    - `UnionMember1`

      - `cron_expression: string`

      - `type: "recurring"`

        - `"recurring"`

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

### Returns

- `ScheduleCreateResponse`

  - `id: string`

  - `next_scheduled_at?: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const schedule = await client.agents.schedule.create('agent_id', {
  messages: [{ content: [{ text: 'text' }], role: 'user' }],
  schedule: { scheduled_at: 0 },
});

console.log(schedule.id);
```

#### Response

```json
{
  "id": "id",
  "next_scheduled_at": "next_scheduled_at"
}
```
