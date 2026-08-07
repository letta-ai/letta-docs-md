## Send Message to Environment

**post** `/v1/environments/{connectionId}/messages`

Send a message to a specific environment connection

### Path Parameters

- `connectionId: string`

### Body Parameters

- `messages: array of object { client_message_id, content, role, otid }  or object { approvals, type }`

  - `object { client_message_id, content, role, otid }`

    - `client_message_id: string`

    - `content: string or array of object { text, type }`

      - `string`

      - `array of object { text, type }`

        - `text: string`

        - `type: "text"`

          - `"text"`

    - `role: "user"`

      - `"user"`

    - `otid: optional string`

  - `object { approvals, type }`

    - `approvals: array of object { status, tool_call_id, tool_return, 3 more }  or object { approve, tool_call_id, reason, 2 more }`

      - `object { status, tool_call_id, tool_return, 3 more }`

        - `status: "success" or "error"`

          - `"success"`

          - `"error"`

        - `tool_call_id: string`

        - `tool_return: string or array of object { text, type }`

          - `string`

          - `array of object { text, type }`

            - `text: string`

            - `type: "text"`

              - `"text"`

        - `stderr: optional array of string`

        - `stdout: optional array of string`

        - `type: optional "tool"`

          - `"tool"`

      - `object { approve, tool_call_id, reason, 2 more }`

        - `approve: boolean`

        - `tool_call_id: string`

        - `reason: optional string`

        - `type: optional "approval"`

          - `"approval"`

        - `updated_input: optional map[unknown]`

    - `type: "approval"`

      - `"approval"`

- `agentId: optional string`

- `conversationId: optional string`

### Returns

- `message: string`

- `success: boolean`

### Example

```http
curl https://api.letta.com/v1/environments/$CONNECTION_ID/messages \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "messages": [
            {
              "client_message_id": "client_message_id",
              "content": "string",
              "role": "user"
            }
          ]
        }'
```

#### Response

```json
{
  "message": "message",
  "success": true
}
```
