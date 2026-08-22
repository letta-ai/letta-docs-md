## Send Message to Environment

`client.environments.sendMessage(stringconnectionID, EnvironmentSendMessageParamsbody, RequestOptionsoptions?): EnvironmentSendMessageResponse`

**post** `/v1/environments/{connectionId}/messages`

Send a message to a specific environment connection

### Parameters

- `connectionID: string`

- `body: EnvironmentSendMessageParams`

  - `messages: Array<UnionMember0 | UnionMember1>`

    - `UnionMember0`

      - `client_message_id: string`

      - `content: string | Array<UnionMember1>`

        - `string`

        - `Array<UnionMember1>`

          - `text: string`

          - `type: "text"`

            - `"text"`

      - `role: "user"`

        - `"user"`

      - `otid?: string`

    - `UnionMember1`

      - `approvals: Array<UnionMember0 | UnionMember1>`

        - `UnionMember0`

          - `status: "success" | "error"`

            - `"success"`

            - `"error"`

          - `tool_call_id: string`

          - `tool_return: string | Array<UnionMember1>`

            - `string`

            - `Array<UnionMember1>`

              - `text: string`

              - `type: "text"`

                - `"text"`

          - `stderr?: Array<string> | null`

          - `stdout?: Array<string> | null`

          - `type?: "tool"`

            - `"tool"`

        - `UnionMember1`

          - `approve: boolean`

          - `tool_call_id: string`

          - `reason?: string | null`

          - `type?: "approval"`

            - `"approval"`

          - `updated_input?: Record<string, unknown> | null`

      - `type: "approval"`

        - `"approval"`

  - `agentId?: string`

  - `conversationId?: string | null`

### Returns

- `EnvironmentSendMessageResponse`

  - `message: string`

  - `success: boolean`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.environments.sendMessage('connectionId', {
  messages: [
    {
      client_message_id: 'client_message_id',
      content: 'string',
      role: 'user',
    },
  ],
});

console.log(response.message);
```

#### Response

```json
{
  "message": "message",
  "success": true
}
```
