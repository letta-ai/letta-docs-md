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
