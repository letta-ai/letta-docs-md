## Delete Passage From Archive

`client.archives.passages.delete(stringpassageID, PassageDeleteParamsparams, RequestOptionsoptions?): void`

**delete** `/v1/archives/{archive_id}/passages/{passage_id}`

Delete a passage from an archive.

This permanently removes the passage from both the database and vector storage (if applicable).

### Parameters

- `passageID: string`

  The ID of the passage in the format 'passage-<uuid4>'

- `params: PassageDeleteParams`

  - `archive_id: string`

    The ID of the archive in the format 'archive-<uuid4>'

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

await client.archives.passages.delete('passage-123e4567-e89b-42d3-8456-426614174000', {
  archive_id: 'archive-123e4567-e89b-42d3-8456-426614174000',
});
```
