# Client

## Check Health

`health()  -> HealthResponse`

**get** `/v1/health/`

Liveness endpoint; returns 200 when process is responsive.

### Returns

- `class HealthResponse: …`

  Health check response body

  - `status: str`

  - `version: str`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.health()
print(response.status)
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

- `class HealthResponse: …`

  Health check response body

  - `status: str`

  - `version: str`
