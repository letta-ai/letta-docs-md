# Client

## Check Health

`client.health(RequestOptionsoptions?): HealthResponse`

**get** `/v1/health/`

Liveness endpoint; returns 200 when process is responsive.

### Returns

- `HealthResponse`

  Health check response body

  - `status: string`

  - `version: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.health();

console.log(response.status);
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

- `HealthResponse`

  Health check response body

  - `status: string`

  - `version: string`
