## List Files For Folder

`client.folders.files.list(stringfolderID, FileListParamsquery?, RequestOptionsoptions?): ArrayPage<FileListResponse>`

**get** `/v1/folders/{folder_id}/files`

List paginated files associated with a data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `query: FileListParams`

  - `after?: string | null`

    Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

  - `include_content?: boolean`

    Whether to include full file content

  - `limit?: number | null`

    Maximum number of files to return

  - `order?: "asc" | "desc"`

    Sort order for files by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `FileListResponse`

  Representation of a single FileMetadata

  - `id: string`

    The human-friendly ID of the File

  - `source_id: string`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded?: number | null`

    Number of chunks that have been embedded.

  - `content?: string | null`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at?: string | null`

    The creation date of the file.

  - `error_message?: string | null`

    Optional error message if the file failed processing.

  - `file_creation_date?: string | null`

    The creation date of the file.

  - `file_last_modified_date?: string | null`

    The last modified date of the file.

  - `file_name?: string | null`

    The name of the file.

  - `file_path?: string | null`

    The path to the file.

  - `file_size?: number | null`

    The size of the file in bytes.

  - `file_type?: string | null`

    The type of the file (MIME type).

  - `original_file_name?: string | null`

    The original name of the file as uploaded.

  - `processing_status?: "pending" | "parsing" | "embedding" | 2 more`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks?: number | null`

    Total number of chunks for the file.

  - `updated_at?: string | null`

    The update date of the file.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const fileListResponse of client.folders.files.list(
  'source-123e4567-e89b-42d3-8456-426614174000',
)) {
  console.log(fileListResponse.id);
}
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
