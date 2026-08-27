# Files

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

## List Files For Folder

`folders.files.list(strfolder_id, FileListParams**kwargs)  -> SyncArrayPage[FileListResponse]`

**get** `/v1/folders/{folder_id}/files`

List paginated files associated with a data folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `after: Optional[str]`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `include_content: Optional[bool]`

  Whether to include full file content

- `limit: Optional[int]`

  Maximum number of files to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for files by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `class FileListResponse: …`

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
page = client.folders.files.list(
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
page = page.items[0]
print(page.id)
```

#### Response

```json
[
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
]
```

## Retrieve File

`folders.files.retrieve(strfile_id, FileRetrieveParams**kwargs)  -> FileRetrieveResponse`

**get** `/v1/folders/{folder_id}/files/{file_id}`

Retrieve a file from a folder by ID.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `file_id: str`

  The ID of the file in the format 'file-<uuid4>'

- `include_content: Optional[bool]`

  Whether to include full file content

### Returns

- `class FileRetrieveResponse: …`

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
file = client.folders.files.retrieve(
    file_id="file-123e4567-e89b-42d3-8456-426614174000",
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
print(file.id)
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

## Domain Types

### File Upload Response

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

### File List Response

- `class FileListResponse: …`

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

### File Retrieve Response

- `class FileRetrieveResponse: …`

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
