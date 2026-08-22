# Access Tokens

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

## Create token  (Cloud-only)

`client.accessTokens.create(AccessTokenCreateParamsbody, RequestOptionsoptions?): AccessTokenCreateResponse`

**post** `/v1/client-side-access-tokens`

Create a new client side access token with the specified configuration.

### Parameters

- `body: AccessTokenCreateParams`

  - `hostname: string`

    The hostname of the client side application. Please specify the full URL including the protocol (http or https).

  - `policy: Array<Policy>`

    - `id: string`

    - `access: Array<"read_messages" | "write_messages" | "read_agent" | "write_agent">`

      - `"read_messages"`

      - `"write_messages"`

      - `"read_agent"`

      - `"write_agent"`

    - `type: "agent"`

      - `"agent"`

  - `expires_at?: string`

    The expiration date of the token. If not provided, the token will expire in 5 minutes

### Returns

- `AccessTokenCreateResponse`

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

const accessToken = await client.accessTokens.create({
  hostname: 'https://example.com',
  policy: [
    {
      id: 'id',
      access: ['read_messages'],
      type: 'agent',
    },
  ],
});

console.log(accessToken.token);
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

`client.accessTokens.delete(stringtoken, AccessTokenDeleteParamsparams?, RequestOptionsoptions?): AccessTokenDeleteResponse`

**delete** `/v1/client-side-access-tokens/{token}`

Delete a client side access token.

### Parameters

- `token: string`

- `params: AccessTokenDeleteParams`

  - `body?: unknown`

### Returns

- `AccessTokenDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const accessToken = await client.accessTokens.delete('token');

console.log(accessToken);
```

#### Response

```json
{}
```

## Domain Types

### Access Token List Response

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

### Access Token Create Response

- `AccessTokenCreateResponse`

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

### Access Token Delete Response

- `AccessTokenDeleteResponse = unknown`
