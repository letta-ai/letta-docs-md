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
