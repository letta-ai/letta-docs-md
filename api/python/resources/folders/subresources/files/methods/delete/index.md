## Delete File From Folder

`folders.files.delete(strfile_id, FileDeleteParams**kwargs)`

**delete** `/v1/folders/{folder_id}/{file_id}`

Delete a file from a folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `file_id: str`

  The ID of the file in the format 'file-<uuid4>'

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
client.folders.files.delete(
    file_id="file-123e4567-e89b-42d3-8456-426614174000",
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
```
