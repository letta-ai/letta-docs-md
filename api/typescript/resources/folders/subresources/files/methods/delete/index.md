## Delete File From Folder

`client.folders.files.delete(stringfileID, FileDeleteParamsparams, RequestOptionsoptions?): void`

**delete** `/v1/folders/{folder_id}/{file_id}`

Delete a file from a folder.

### Parameters

- `fileID: string`

  The ID of the file in the format 'file-<uuid4>'

- `params: FileDeleteParams`

  - `folder_id: string`

    The ID of the source in the format 'source-<uuid4>'

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

await client.folders.files.delete('file-123e4567-e89b-42d3-8456-426614174000', {
  folder_id: 'source-123e4567-e89b-42d3-8456-426614174000',
});
```
