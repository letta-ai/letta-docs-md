## Delete Folder

`client.folders.delete(stringfolderID, RequestOptionsoptions?): FolderDeleteResponse`

**delete** `/v1/folders/{folder_id}`

Delete a data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

### Returns

- `FolderDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const folder = await client.folders.delete('source-123e4567-e89b-42d3-8456-426614174000');

console.log(folder);
```

#### Response

```json
{}
```
