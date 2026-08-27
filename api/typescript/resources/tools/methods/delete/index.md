## Delete Tool

`client.tools.delete(stringtoolID, RequestOptionsoptions?): ToolDeleteResponse`

**delete** `/v1/tools/{tool_id}`

Delete a tool by name

### Parameters

- `toolID: string`

  The ID of the tool in the format 'tool-<uuid4>'

### Returns

- `ToolDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const tool = await client.tools.delete('tool-123e4567-e89b-42d3-8456-426614174000');

console.log(tool);
```

#### Response

```json
{}
```
