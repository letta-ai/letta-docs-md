## List tokens  (Cloud-only)

`client.accessTokens.list(AccessTokenListParamsquery?, RequestOptionsoptions?): AccessTokenListResponse`

**get** `/v1/client-side-access-tokens`

List all client side access tokens for the current account. This is only available for cloud users.

### Parameters

- `query: AccessTokenListParams`

  - `agentId?: string`

    The agent ID to filter tokens by. If provided, only tokens for this agent will be returned.

  - `limit?: number`

    The number of tokens to return per page. Defaults to 10.

  - `offset?: number`

    The offset for pagination. Defaults to 0.

### Returns

- `AccessTokenListResponse`

  - `hasNextPage: boolean`

  - `tokens: Array<Token>`

    - `token: string`

    - `expiresAt: string`

    - `hostname: string`

    - `policy: Policy`

      - `data: Array<Data>`

        - `id: string`

        - `access: Array<"read_messages" | "write_messages" | "read_agent" | "write_agent">`

          - `"read_messages"`

          - `"write_messages"`

          - `"read_agent"`

          - `"write_agent"`

        - `type: "agent"`

          - `"agent"`

      - `version: "1"`

        - `"1"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const accessTokens = await client.accessTokens.list();

console.log(accessTokens.hasNextPage);
```

#### Response

```json
{
  "hasNextPage": true,
  "tokens": [
    {
      "token": "token",
      "expiresAt": "expiresAt",
      "hostname": "hostname",
      "policy": {
        "data": [
          {
            "id": "id",
            "access": [
              "read_messages"
            ],
            "type": "agent"
          }
        ],
        "version": "1"
      }
    }
  ]
}
```
