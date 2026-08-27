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
