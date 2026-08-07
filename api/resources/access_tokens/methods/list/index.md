## List tokens  (Cloud-only)

**get** `/v1/client-side-access-tokens`

List all client side access tokens for the current account. This is only available for cloud users.

### Query Parameters

- `agentId: optional string`

  The agent ID to filter tokens by. If provided, only tokens for this agent will be returned.

- `limit: optional number`

  The number of tokens to return per page. Defaults to 10.

- `offset: optional number`

  The offset for pagination. Defaults to 0.

### Returns

- `hasNextPage: boolean`

- `tokens: array of object { token, expiresAt, hostname, policy }`

  - `token: string`

  - `expiresAt: string`

  - `hostname: string`

  - `policy: object { data, version }`

    - `data: array of object { id, access, type }`

      - `id: string`

      - `access: array of "read_messages" or "write_messages" or "read_agent" or "write_agent"`

        - `"read_messages"`

        - `"write_messages"`

        - `"read_agent"`

        - `"write_agent"`

      - `type: "agent"`

        - `"agent"`

    - `version: "1"`

      - `"1"`

### Example

```http
curl https://api.letta.com/v1/client-side-access-tokens \
    -H "Authorization: Bearer $LETTA_API_KEY"
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
