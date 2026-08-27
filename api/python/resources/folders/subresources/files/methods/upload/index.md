## Upload File To Folder

`folders.files.upload(strfolder_id, FileUploadParams**kwargs)  -> FileUploadResponse`

**post** `/v1/folders/{folder_id}/upload`

Upload a file to a data folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `file: FileTypes`

- `duplicate_handling: Optional[Literal["skip", "error", "suffix", "replace"]]`

  How to handle duplicate filenames

  - `"skip"`

  - `"error"`

  - `"suffix"`

  - `"replace"`

- `name: Optional[str]`

  Optional custom name to override the uploaded file's name

### Returns

- `class FileUploadResponse: …`

  Representation of a single FileMetadata

  - `id: str`

    The human-friendly ID of the File

  - `source_id: str`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded: Optional[int]`

    Number of chunks that have been embedded.

  - `content: Optional[str]`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at: Optional[datetime]`

    The creation date of the file.

  - `error_message: Optional[str]`

    Optional error message if the file failed processing.

  - `file_creation_date: Optional[str]`

    The creation date of the file.

  - `file_last_modified_date: Optional[str]`

    The last modified date of the file.

  - `file_name: Optional[str]`

    The name of the file.

  - `file_path: Optional[str]`

    The path to the file.

  - `file_size: Optional[int]`

    The size of the file in bytes.

  - `file_type: Optional[str]`

    The type of the file (MIME type).

  - `original_file_name: Optional[str]`

    The original name of the file as uploaded.

  - `processing_status: Optional[Literal["pending", "parsing", "embedding", 2 more]]`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks: Optional[int]`

    Total number of chunks for the file.

  - `updated_at: Optional[datetime]`

    The update date of the file.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.folders.files.upload(
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
    file=b"Example data",
)
print(response.id)
```

#### Response

```json
{
  "id": "file-123e4567-e89b-12d3-a456-426614174000",
  "source_id": "source_id",
  "chunks_embedded": 0,
  "content": "content",
  "created_at": "2019-12-27T18:11:19.117Z",
  "error_message": "error_message",
  "file_creation_date": "file_creation_date",
  "file_last_modified_date": "file_last_modified_date",
  "file_name": "file_name",
  "file_path": "file_path",
  "file_size": 0,
  "file_type": "file_type",
  "original_file_name": "original_file_name",
  "processing_status": "pending",
  "total_chunks": 0,
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```
