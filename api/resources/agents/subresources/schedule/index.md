# Schedule

## Schedule Agent Message

**post** `/v1/agents/{agent_id}/schedule`

Schedule a message to be sent by the agent at a specified time or on a recurring basis.

### Path Parameters

- `agent_id: string`

### Body Parameters

- `messages: array of object { content, role, name, 3 more }`

  - `content: array of object { text, signature, type }  or object { source, type }  or string`

    - `array of object { text, signature, type }  or object { source, type }`

      - `object { text, signature, type }`

        - `text: string`

        - `signature: optional string`

        - `type: optional "text"`

          - `"text"`

      - `object { source, type }`

        - `source: object { data, media_type, detail, type }`

          - `data: string`

          - `media_type: string`

          - `detail: optional string`

          - `type: optional "base64"`

            - `"base64"`

        - `type: "image"`

          - `"image"`

    - `string`

  - `role: "user" or "assistant" or "system"`

    - `"user"`

    - `"assistant"`

    - `"system"`

  - `name: optional string`

  - `otid: optional string`

  - `sender_id: optional string`

  - `type: optional "message"`

    - `"message"`

- `schedule: object { scheduled_at, type }  or object { cron_expression, type }`

  - `object { scheduled_at, type }`

    - `scheduled_at: number`

    - `type: optional "one-time"`

      - `"one-time"`

  - `object { cron_expression, type }`

    - `cron_expression: string`

    - `type: "recurring"`

      - `"recurring"`

- `callback_url: optional string`

- `include_return_message_types: optional array of "system_message" or "user_message" or "assistant_message" or 6 more`

  - `"system_message"`

  - `"user_message"`

  - `"assistant_message"`

  - `"reasoning_message"`

  - `"hidden_reasoning_message"`

  - `"tool_call_message"`

  - `"tool_return_message"`

  - `"approval_request_message"`

  - `"approval_response_message"`

- `max_steps: optional number`

### Returns

- `id: string`

- `next_scheduled_at: optional string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/schedule \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "messages": [
            {
              "content": [
                {
                  "text": "text"
                }
              ],
              "role": "user"
            }
          ],
          "schedule": {
            "scheduled_at": 0
          }
        }'
```

#### Response

```json
{
  "id": "id",
  "next_scheduled_at": "next_scheduled_at"
}
```

## List Scheduled Agent Messages

**get** `/v1/agents/{agent_id}/schedule`

List all scheduled messages for a specific agent.

### Path Parameters

- `agent_id: string`

### Query Parameters

- `after: optional string`

- `limit: optional string`

### Returns

- `has_next_page: boolean`

- `scheduled_messages: array of object { id, agent_id, message, 2 more }`

  - `id: string`

  - `agent_id: string`

  - `message: object { messages, callback_url, include_return_message_types, max_steps }`

    - `messages: array of object { content, role, name, 3 more }`

      - `content: array of object { text, signature, type }  or object { source, type }  or string`

        - `array of object { text, signature, type }  or object { source, type }`

          - `object { text, signature, type }`

            - `text: string`

            - `signature: optional string`

            - `type: optional "text"`

              - `"text"`

          - `object { source, type }`

            - `source: object { data, media_type, detail, type }`

              - `data: string`

              - `media_type: string`

              - `detail: optional string`

              - `type: optional "base64"`

                - `"base64"`

            - `type: "image"`

              - `"image"`

        - `string`

      - `role: "user" or "assistant" or "system"`

        - `"user"`

        - `"assistant"`

        - `"system"`

      - `name: optional string`

      - `otid: optional string`

      - `sender_id: optional string`

      - `type: optional "message"`

        - `"message"`

    - `callback_url: optional string`

    - `include_return_message_types: optional array of "system_message" or "user_message" or "assistant_message" or 6 more`

      - `"system_message"`

      - `"user_message"`

      - `"assistant_message"`

      - `"reasoning_message"`

      - `"hidden_reasoning_message"`

      - `"tool_call_message"`

      - `"tool_return_message"`

      - `"approval_request_message"`

      - `"approval_response_message"`

    - `max_steps: optional number`

  - `next_scheduled_time: string`

  - `schedule: object { scheduled_at, type }  or object { cron_expression, type }`

    - `object { scheduled_at, type }`

      - `scheduled_at: number`

      - `type: optional "one-time"`

        - `"one-time"`

    - `object { cron_expression, type }`

      - `cron_expression: string`

      - `type: "recurring"`

        - `"recurring"`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/schedule \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

**get** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Retrieve a scheduled message by its ID for a specific agent.

### Path Parameters

- `agent_id: string`

- `scheduled_message_id: string`

### Returns

- `id: string`

- `agent_id: string`

- `message: object { messages, callback_url, include_return_message_types, max_steps }`

  - `messages: array of object { content, role, name, 3 more }`

    - `content: array of object { text, signature, type }  or object { source, type }  or string`

      - `array of object { text, signature, type }  or object { source, type }`

        - `object { text, signature, type }`

          - `text: string`

          - `signature: optional string`

          - `type: optional "text"`

            - `"text"`

        - `object { source, type }`

          - `source: object { data, media_type, detail, type }`

            - `data: string`

            - `media_type: string`

            - `detail: optional string`

            - `type: optional "base64"`

              - `"base64"`

          - `type: "image"`

            - `"image"`

      - `string`

    - `role: "user" or "assistant" or "system"`

      - `"user"`

      - `"assistant"`

      - `"system"`

    - `name: optional string`

    - `otid: optional string`

    - `sender_id: optional string`

    - `type: optional "message"`

      - `"message"`

  - `callback_url: optional string`

  - `include_return_message_types: optional array of "system_message" or "user_message" or "assistant_message" or 6 more`

    - `"system_message"`

    - `"user_message"`

    - `"assistant_message"`

    - `"reasoning_message"`

    - `"hidden_reasoning_message"`

    - `"tool_call_message"`

    - `"tool_return_message"`

    - `"approval_request_message"`

    - `"approval_response_message"`

  - `max_steps: optional number`

- `next_scheduled_time: string`

- `schedule: object { scheduled_at, type }  or object { cron_expression, type }`

  - `object { scheduled_at, type }`

    - `scheduled_at: number`

    - `type: optional "one-time"`

      - `"one-time"`

  - `object { cron_expression, type }`

    - `cron_expression: string`

    - `type: "recurring"`

      - `"recurring"`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/schedule/$SCHEDULED_MESSAGE_ID \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

**delete** `/v1/agents/{agent_id}/schedule/{scheduled_message_id}`

Delete a scheduled message by its ID for a specific agent.

### Path Parameters

- `agent_id: string`

- `scheduled_message_id: string`

### Returns

- `success: true`

  - `true`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/schedule/$SCHEDULED_MESSAGE_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "success": true
}
```

## Domain Types

### Schedule Create Response

- `ScheduleCreateResponse object { id, next_scheduled_at }`

  - `id: string`

  - `next_scheduled_at: optional string`

### Schedule List Response

- `ScheduleListResponse object { has_next_page, scheduled_messages }`

  - `has_next_page: boolean`

  - `scheduled_messages: array of object { id, agent_id, message, 2 more }`

    - `id: string`

    - `agent_id: string`

    - `message: object { messages, callback_url, include_return_message_types, max_steps }`

      - `messages: array of object { content, role, name, 3 more }`

        - `content: array of object { text, signature, type }  or object { source, type }  or string`

          - `array of object { text, signature, type }  or object { source, type }`

            - `object { text, signature, type }`

              - `text: string`

              - `signature: optional string`

              - `type: optional "text"`

                - `"text"`

            - `object { source, type }`

              - `source: object { data, media_type, detail, type }`

                - `data: string`

                - `media_type: string`

                - `detail: optional string`

                - `type: optional "base64"`

                  - `"base64"`

              - `type: "image"`

                - `"image"`

          - `string`

        - `role: "user" or "assistant" or "system"`

          - `"user"`

          - `"assistant"`

          - `"system"`

        - `name: optional string`

        - `otid: optional string`

        - `sender_id: optional string`

        - `type: optional "message"`

          - `"message"`

      - `callback_url: optional string`

      - `include_return_message_types: optional array of "system_message" or "user_message" or "assistant_message" or 6 more`

        - `"system_message"`

        - `"user_message"`

        - `"assistant_message"`

        - `"reasoning_message"`

        - `"hidden_reasoning_message"`

        - `"tool_call_message"`

        - `"tool_return_message"`

        - `"approval_request_message"`

        - `"approval_response_message"`

      - `max_steps: optional number`

    - `next_scheduled_time: string`

    - `schedule: object { scheduled_at, type }  or object { cron_expression, type }`

      - `object { scheduled_at, type }`

        - `scheduled_at: number`

        - `type: optional "one-time"`

          - `"one-time"`

      - `object { cron_expression, type }`

        - `cron_expression: string`

        - `type: "recurring"`

          - `"recurring"`

### Schedule Retrieve Response

- `ScheduleRetrieveResponse object { id, agent_id, message, 2 more }`

  - `id: string`

  - `agent_id: string`

  - `message: object { messages, callback_url, include_return_message_types, max_steps }`

    - `messages: array of object { content, role, name, 3 more }`

      - `content: array of object { text, signature, type }  or object { source, type }  or string`

        - `array of object { text, signature, type }  or object { source, type }`

          - `object { text, signature, type }`

            - `text: string`

            - `signature: optional string`

            - `type: optional "text"`

              - `"text"`

          - `object { source, type }`

            - `source: object { data, media_type, detail, type }`

              - `data: string`

              - `media_type: string`

              - `detail: optional string`

              - `type: optional "base64"`

                - `"base64"`

            - `type: "image"`

              - `"image"`

        - `string`

      - `role: "user" or "assistant" or "system"`

        - `"user"`

        - `"assistant"`

        - `"system"`

      - `name: optional string`

      - `otid: optional string`

      - `sender_id: optional string`

      - `type: optional "message"`

        - `"message"`

    - `callback_url: optional string`

    - `include_return_message_types: optional array of "system_message" or "user_message" or "assistant_message" or 6 more`

      - `"system_message"`

      - `"user_message"`

      - `"assistant_message"`

      - `"reasoning_message"`

      - `"hidden_reasoning_message"`

      - `"tool_call_message"`

      - `"tool_return_message"`

      - `"approval_request_message"`

      - `"approval_response_message"`

    - `max_steps: optional number`

  - `next_scheduled_time: string`

  - `schedule: object { scheduled_at, type }  or object { cron_expression, type }`

    - `object { scheduled_at, type }`

      - `scheduled_at: number`

      - `type: optional "one-time"`

        - `"one-time"`

    - `object { cron_expression, type }`

      - `cron_expression: string`

      - `type: "recurring"`

        - `"recurring"`

### Schedule Delete Response

- `ScheduleDeleteResponse object { success }`

  - `success: true`

    - `true`
