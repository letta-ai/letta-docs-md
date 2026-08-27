## Delete Passage From Archive

`archives.passages.delete(strpassage_id, PassageDeleteParams**kwargs)`

**delete** `/v1/archives/{archive_id}/passages/{passage_id}`

Delete a passage from an archive.

This permanently removes the passage from both the database and vector storage (if applicable).

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

- `passage_id: str`

  The ID of the passage in the format 'passage-<uuid4>'

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
client.archives.passages.delete(
    passage_id="passage-123e4567-e89b-42d3-8456-426614174000",
    archive_id="archive-123e4567-e89b-42d3-8456-426614174000",
)
```
