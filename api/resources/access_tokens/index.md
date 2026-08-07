# Access Tokens

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

## Create token  (Cloud-only)

**post** `/v1/client-side-access-tokens`

Create a new client side access token with the specified configuration.

### Body Parameters

- `hostname: string`

  The hostname of the client side application. Please specify the full URL including the protocol (http or https).

- `policy: array of object { id, access, type }`

  - `id: string`

  - `access: array of "read_messages" or "write_messages" or "read_agent" or "write_agent"`

    - `"read_messages"`

    - `"write_messages"`

    - `"read_agent"`

    - `"write_agent"`

  - `type: "agent"`

    - `"agent"`

- `expires_at: optional string`

  The expiration date of the token. If not provided, the token will expire in 5 minutes

### Returns

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
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "hostname": "https://example.com",
          "policy": [
            {
              "id": "id",
              "access": [
                "read_messages"
              ],
              "type": "agent"
            }
          ]
        }'
```

#### Response

```json
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
```

## Delete token  (Cloud-only)

**delete** `/v1/client-side-access-tokens/{token}`

Delete a client side access token.

### Path Parameters

- `token: string`

### Body Parameters

- `body: optional unknown`

### Example

```http
curl https://api.letta.com/v1/client-side-access-tokens/$TOKEN \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## Domain Types

### Access Token List Response

- `AccessTokenListResponse object { hasNextPage, tokens }`

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

### Access Token Create Response

- `AccessTokenCreateResponse object { token, expiresAt, hostname, policy }`

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

### Access Token Delete Response

- `AccessTokenDeleteResponse = unknown`
