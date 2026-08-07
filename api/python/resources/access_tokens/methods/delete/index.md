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
