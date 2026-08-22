## Delete Archive

`archives.delete(strarchive_id)`

**delete** `/v1/archives/{archive_id}`

Delete an archive by its ID.

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
client.archives.delete(
    "archive-123e4567-e89b-42d3-8456-426614174000",
)
```
