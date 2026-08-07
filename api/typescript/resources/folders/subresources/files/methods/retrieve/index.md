## Retrieve File

`client.folders.files.retrieve(stringfileID, FileRetrieveParamsparams, RequestOptionsoptions?): FileRetrieveResponse`

**get** `/v1/folders/{folder_id}/files/{file_id}`

Retrieve a file from a folder by ID.

### Parameters

- `fileID: string`

  The ID of the file in the format 'file-<uuid4>'

- `params: FileRetrieveParams`

  - `folder_id: string`

    Path param: The ID of the source in the format 'source-<uuid4>'

  - `include_content?: boolean`

    Query param: Whether to include full file content

### Returns

- `FileRetrieveResponse`

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

const file = await client.folders.files.retrieve('file-123e4567-e89b-42d3-8456-426614174000', {
  folder_id: 'source-123e4567-e89b-42d3-8456-426614174000',
});

console.log(file.id);
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
