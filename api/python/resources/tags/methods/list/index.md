## List Tags

`tags.list(TagListParams**kwargs)  -> TagListResponse`

**get** `/v1/tags/`

Get the list of all tags (from agents and blocks) that have been created.

### Parameters

- `after: Optional[str]`

  Tag cursor for pagination. Returns tags that come after this tag in the specified sort order

- `before: Optional[str]`

  Tag cursor for pagination. Returns tags that come before this tag in the specified sort order

- `limit: Optional[int]`

  Maximum number of tags to return

- `name: Optional[str]`

  Filter tags by name

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for tags. 'asc' for alphabetical order, 'desc' for reverse alphabetical order

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["name"]]`

  Field to sort by

  - `"name"`

- `query_text: Optional[str]`

  Filter tags by text search. Deprecated, please use name field instead

### Returns

- `List[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
tags = client.tags.list()
print(tags)
```

#### Response

```json
[
  "string"
]
```
