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
