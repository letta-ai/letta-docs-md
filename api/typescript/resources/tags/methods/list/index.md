## List Tags

`client.tags.list(TagListParamsquery?, RequestOptionsoptions?): TagListResponse`

**get** `/v1/tags/`

Get the list of all tags (from agents and blocks) that have been created.

### Parameters

- `query: TagListParams`

  - `after?: string | null`

    Tag cursor for pagination. Returns tags that come after this tag in the specified sort order

  - `before?: string | null`

    Tag cursor for pagination. Returns tags that come before this tag in the specified sort order

  - `limit?: number | null`

    Maximum number of tags to return

  - `name?: string | null`

    Filter tags by name

  - `order?: "asc" | "desc"`

    Sort order for tags. 'asc' for alphabetical order, 'desc' for reverse alphabetical order

    - `"asc"`

    - `"desc"`

  - `order_by?: "name"`

    Field to sort by

    - `"name"`

  - `query_text?: string | null`

    Filter tags by text search. Deprecated, please use name field instead

### Returns

- `TagListResponse = Array<string>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const tags = await client.tags.list();

console.log(tags);
```

#### Response

```json
[
  "string"
]
```
