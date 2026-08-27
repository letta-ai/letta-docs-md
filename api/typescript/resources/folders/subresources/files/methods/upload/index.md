## Upload File To Folder

`client.folders.files.upload(stringfolderID, FileUploadParamsparams, RequestOptionsoptions?): FileUploadResponse`

**post** `/v1/folders/{folder_id}/upload`

Upload a file to a data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `params: FileUploadParams`

  - `file: Uploadable`

    Body param

  - `duplicate_handling?: "skip" | "error" | "suffix" | "replace"`

    Query param: How to handle duplicate filenames

    - `"skip"`

    - `"error"`

    - `"suffix"`

    - `"replace"`

  - `name?: string | null`

    Query param: Optional custom name to override the uploaded file's name

### Returns

- `FileUploadResponse`

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
import fs from 'fs';
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.folders.files.upload('source-123e4567-e89b-42d3-8456-426614174000', {
  file: fs.createReadStream('path/to/file'),
});

console.log(response.id);
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
