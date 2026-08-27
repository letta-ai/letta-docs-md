## Delete Archive

`client.archives.delete(stringarchiveID, RequestOptionsoptions?): void`

**delete** `/v1/archives/{archive_id}`

Delete an archive by its ID.

### Parameters

- `archiveID: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

await client.archives.delete('archive-123e4567-e89b-42d3-8456-426614174000');
```
