# Access Tokens

## List tokens  (Cloud-only)

`access_tokens.list(AccessTokenListParams**kwargs)  -> AccessTokenListResponse`

**get** `/v1/client-side-access-tokens`

List all client side access tokens for the current account. This is only available for cloud users.

### Parameters

- `agent_id: Optional[str]`

  The agent ID to filter tokens by. If provided, only tokens for this agent will be returned.

- `limit: Optional[float]`

  The number of tokens to return per page. Defaults to 10.

- `offset: Optional[float]`

  The offset for pagination. Defaults to 0.

### Returns

- `class AccessTokenListResponse: …`

  - `has_next_page: bool`

  - `tokens: List[Token]`

    - `token: str`

    - `expires_at: str`

    - `hostname: str`

    - `policy: TokenPolicy`

      - `data: List[TokenPolicyData]`

        - `id: str`

        - `access: List[Literal["read_messages", "write_messages", "read_agent", "write_agent"]]`

          - `"read_messages"`

          - `"write_messages"`

          - `"read_agent"`

          - `"write_agent"`

        - `type: Literal["agent"]`

          - `"agent"`

      - `version: Literal["1"]`

        - `"1"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
access_tokens = client.access_tokens.list()
print(access_tokens.has_next_page)
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

`access_tokens.create(AccessTokenCreateParams**kwargs)  -> AccessTokenCreateResponse`

**post** `/v1/client-side-access-tokens`

Create a new client side access token with the specified configuration.

### Parameters

- `hostname: str`

  The hostname of the client side application. Please specify the full URL including the protocol (http or https).

- `policy: Iterable[Policy]`

  - `id: str`

  - `access: List[Literal["read_messages", "write_messages", "read_agent", "write_agent"]]`

    - `"read_messages"`

    - `"write_messages"`

    - `"read_agent"`

    - `"write_agent"`

  - `type: Literal["agent"]`

    - `"agent"`

- `expires_at: Optional[str]`

  The expiration date of the token. If not provided, the token will expire in 5 minutes

### Returns

- `class AccessTokenCreateResponse: …`

  - `token: str`

  - `expires_at: str`

  - `hostname: str`

  - `policy: Policy`

    - `data: List[PolicyData]`

      - `id: str`

      - `access: List[Literal["read_messages", "write_messages", "read_agent", "write_agent"]]`

        - `"read_messages"`

        - `"write_messages"`

        - `"read_agent"`

        - `"write_agent"`

      - `type: Literal["agent"]`

        - `"agent"`

    - `version: Literal["1"]`

      - `"1"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
access_token = client.access_tokens.create(
    hostname="https://example.com",
    policy=[{
        "id": "id",
        "access": ["read_messages"],
        "type": "agent",
    }],
)
print(access_token.token)
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

`access_tokens.delete(strtoken, AccessTokenDeleteParams**kwargs)  -> object`

**delete** `/v1/client-side-access-tokens/{token}`

Delete a client side access token.

### Parameters

- `token: str`

- `body: Optional[object]`

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
access_token = client.access_tokens.delete(
    token="token",
)
print(access_token)
```

#### Response

```json
{}
```

## Domain Types

### Access Token List Response

- `class AccessTokenListResponse: …`

  - `has_next_page: bool`

  - `tokens: List[Token]`

    - `token: str`

    - `expires_at: str`

    - `hostname: str`

    - `policy: TokenPolicy`

      - `data: List[TokenPolicyData]`

        - `id: str`

        - `access: List[Literal["read_messages", "write_messages", "read_agent", "write_agent"]]`

          - `"read_messages"`

          - `"write_messages"`

          - `"read_agent"`

          - `"write_agent"`

        - `type: Literal["agent"]`

          - `"agent"`

      - `version: Literal["1"]`

        - `"1"`

### Access Token Create Response

- `class AccessTokenCreateResponse: …`

  - `token: str`

  - `expires_at: str`

  - `hostname: str`

  - `policy: Policy`

    - `data: List[PolicyData]`

      - `id: str`

      - `access: List[Literal["read_messages", "write_messages", "read_agent", "write_agent"]]`

        - `"read_messages"`

        - `"write_messages"`

        - `"read_agent"`

        - `"write_agent"`

      - `type: Literal["agent"]`

        - `"agent"`

    - `version: Literal["1"]`

      - `"1"`
