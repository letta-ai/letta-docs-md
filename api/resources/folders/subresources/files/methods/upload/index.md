## Upload File To Folder

**post** `/v1/folders/{folder_id}/upload`

Upload a file to a data folder.

### Path Parameters

- `folder_id: string`

  The ID of the source in the format 'source-<uuid4>'

### Query Parameters

- `duplicate_handling: optional "skip" or "error" or "suffix" or "replace"`

  How to handle duplicate filenames

  - `"skip"`

  - `"error"`

  - `"suffix"`

  - `"replace"`

- `name: optional string`

  Optional custom name to override the uploaded file's name

### Returns

- `id: string`

  The human-friendly ID of the File

- `source_id: string`

  Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

- `chunks_embedded: optional number`

  Number of chunks that have been embedded.

- `content: optional string`

  Optional full-text content of the file; only populated on demand due to its size.

- `created_at: optional string`

  The creation date of the file.

- `error_message: optional string`

  Optional error message if the file failed processing.

- `file_creation_date: optional string`

  The creation date of the file.

- `file_last_modified_date: optional string`

  The last modified date of the file.

- `file_name: optional string`

  The name of the file.

- `file_path: optional string`

  The path to the file.

- `file_size: optional number`

  The size of the file in bytes.

- `file_type: optional string`

  The type of the file (MIME type).

- `original_file_name: optional string`

  The original name of the file as uploaded.

- `processing_status: optional "pending" or "parsing" or "embedding" or 2 more`

  The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

  - `"pending"`

  - `"parsing"`

  - `"embedding"`

  - `"completed"`

  - `"error"`

- `total_chunks: optional number`

  Total number of chunks for the file.

- `updated_at: optional string`

  The update date of the file.

### Example

```http
curl https://api.letta.com/v1/folders/$FOLDER_ID/upload \
    -H 'Content-Type: multipart/form-data' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -F 'file=@/path/to/file'
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
