## Delete Folder

`folders.delete(strfolder_id)  -> object`

**delete** `/v1/folders/{folder_id}`

Delete a data folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
folder = client.folders.delete(
    "source-123e4567-e89b-42d3-8456-426614174000",
)
print(folder)
```

#### Response

```json
{}
```
