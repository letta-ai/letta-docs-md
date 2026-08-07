# Schedule

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

## List Scheduled Agent Messages

`client.agents.schedule.list(stringagentID, ScheduleListParamsquery?, RequestOptionsoptions?): ScheduleListResponse`

**get** `/v1/agents/{agent_id}/schedule`

List all scheduled messages for a specific agent.

### Parameters

- `agentID: string`

- `query: ScheduleListParams`

  - `after?: string`

  - `limit?: string`

### Returns

- `ScheduleListResponse`

  - `has_next_page: boolean`

  - `scheduled_messages: Array<ScheduledMessage>`

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

const schedules = await client.agents.schedule.list('agent_id');

console.log(schedules.has_next_page);
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

## Delete Scheduled Agent Message

`client.agents.schedule.delete(stringscheduledMessageID, ScheduleDeleteParamsparams, RequestOptionsoptions?): ScheduleDeleteResponse`

**delete** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Delete a scheduled message by its ID for a specific agent.

### Parameters

- `scheduledMessageID: string`

- `params: ScheduleDeleteParams`

  - `agent_id: string`

### Returns

- `ScheduleDeleteResponse`

  - `success: true`

    - `true`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const schedule = await client.agents.schedule.delete('scheduled_message_id', {
  agent_id: 'agent_id',
});

console.log(schedule.success);
```

#### Response

```json
{
  "success": true
}
```

## Domain Types

### Schedule Create Response

- `ScheduleCreateResponse`

  - `id: string`

  - `next_scheduled_at?: string`

### Schedule List Response

- `ScheduleListResponse`

  - `has_next_page: boolean`

  - `scheduled_messages: Array<ScheduledMessage>`

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

### Schedule Retrieve Response

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

### Schedule Delete Response

- `ScheduleDeleteResponse`

  - `success: true`

    - `true`
