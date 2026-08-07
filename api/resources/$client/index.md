# Client

## Check Health

**get** `/v1/health/`

Liveness endpoint; returns 200 when process is responsive.

### Returns

- `status: string`

- `version: string`

### Example

```http
curl https://api.letta.com/v1/health/ \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "status": "status",
  "version": "version"
}
```

## Domain Types

### Health Response

- `HealthResponse object { status, version }`

  Health check response body

  - `status: string`

  - `version: string`
