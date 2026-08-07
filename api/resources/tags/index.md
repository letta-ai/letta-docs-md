# Tags

## List Tags

**get** `/v1/tags/`

Get the list of all tags (from agents and blocks) that have been created.

### Query Parameters

- `after: optional string`

  Tag cursor for pagination. Returns tags that come after this tag in the specified sort order

- `before: optional string`

  Tag cursor for pagination. Returns tags that come before this tag in the specified sort order

- `limit: optional number`

  Maximum number of tags to return

- `name: optional string`

  Filter tags by name

- `order: optional "asc" or "desc"`

  Sort order for tags. 'asc' for alphabetical order, 'desc' for reverse alphabetical order

  - `"asc"`

  - `"desc"`

- `order_by: optional "name"`

  Field to sort by

  - `"name"`

- `query_text: optional string`

  Filter tags by text search. Deprecated, please use name field instead

### Example

```http
curl https://api.letta.com/v1/tags/ \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  "string"
]
```

## Domain Types

### Tag List Response

- `TagListResponse = array of string`
