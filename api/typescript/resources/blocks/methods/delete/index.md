## Delete Block

`client.blocks.delete(stringblockID, RequestOptionsoptions?): BlockDeleteResponse`

**delete** `/v1/blocks/{block_id}`

Delete Block

### Parameters

- `blockID: string`

  The ID of the block in the format 'block-<uuid4>'

### Returns

- `BlockDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const block = await client.blocks.delete('block-123e4567-e89b-42d3-8456-426614174000');

console.log(block);
```

#### Response

```json
{}
```
