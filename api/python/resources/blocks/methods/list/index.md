## List Blocks

`blocks.list(BlockListParams**kwargs)  -> SyncArrayPage[BlockResponse]`

**get** `/v1/blocks/`

List Blocks

### Parameters

- `after: Optional[str]`

  Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

- `connected_to_agents_count_eq: Optional[Iterable[int]]`

  Filter blocks by the exact number of connected agents. If provided, returns blocks that have exactly this number of connected agents.

- `connected_to_agents_count_gt: Optional[int]`

  Filter blocks by the number of connected agents. If provided, returns blocks that have more than this number of connected agents.

- `connected_to_agents_count_lt: Optional[int]`

  Filter blocks by the number of connected agents. If provided, returns blocks that have less than this number of connected agents.

- `description_search: Optional[str]`

  Search blocks by description. If provided, returns blocks whose description matches the search query. This is a full-text search on block descriptions.

- `identifier_keys: Optional[Sequence[str]]`

  Search agents by identifier keys

- `identity_id: Optional[str]`

  The ID of the identity in the format 'identity-<uuid4>'

- `label: Optional[str]`

  Label to include (alphanumeric, hyphens, underscores, forward slashes)

- `label_search: Optional[str]`

  Search blocks by label. If provided, returns blocks whose label matches the search query. This is a full-text search on block labels.

- `limit: Optional[int]`

  Number of blocks to return

- `match_all_tags: Optional[bool]`

  If True, only returns blocks that match ALL given tags. Otherwise, return blocks that have ANY of the passed-in tags.

- `name: Optional[str]`

  Name filter (alphanumeric, spaces, hyphens, underscores)

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for blocks by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

- `project_id: Optional[str]`

  Search blocks by project id

- `tags: Optional[Sequence[str]]`

  List of tags to filter blocks by

- `templates_only: Optional[bool]`

  Whether to include only templates

- `value_search: Optional[str]`

  Search blocks by value. If provided, returns blocks whose value matches the search query. This is a full-text search on block values.

### Returns

- `class BlockResponse: …`

  - `id: str`

    The id of the block.

  - `value: str`

    Value of the block.

  - `base_template_id: Optional[str]`

    (Deprecated) The base template id of the block.

  - `created_by_id: Optional[str]`

    The id of the user that made this Block.

  - `deployment_id: Optional[str]`

    (Deprecated) The id of the deployment.

  - `description: Optional[str]`

    Description of the block.

  - `entity_id: Optional[str]`

    (Deprecated) The id of the entity within the template.

  - `hidden: Optional[bool]`

    (Deprecated) If set to True, the block will be hidden.

  - `is_template: Optional[bool]`

    Whether the block is a template (e.g. saved human/persona options).

  - `label: Optional[str]`

    Label of the block (e.g. 'human', 'persona') in the context window.

  - `last_updated_by_id: Optional[str]`

    The id of the user that last updated this Block.

  - `limit: Optional[int]`

    Character limit of the block.

  - `metadata: Optional[Dict[str, object]]`

    Metadata of the block.

  - `preserve_on_migration: Optional[bool]`

    (Deprecated) Preserve the block on template migration.

  - `project_id: Optional[str]`

    The associated project id.

  - `read_only: Optional[bool]`

    (Deprecated) Whether the agent has read-only access to the block.

  - `tags: Optional[List[str]]`

    The tags associated with the block.

  - `template_id: Optional[str]`

    (Deprecated) The id of the template.

  - `template_name: Optional[str]`

    (Deprecated) The name of the block template (if it is a template).

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.blocks.list()
page = page.items[0]
print(page.id)
```

#### Response

```json
[
  {
    "id": "id",
    "value": "value",
    "base_template_id": "base_template_id",
    "created_by_id": "created_by_id",
    "deployment_id": "deployment_id",
    "description": "description",
    "entity_id": "entity_id",
    "hidden": true,
    "is_template": true,
    "label": "label",
    "last_updated_by_id": "last_updated_by_id",
    "limit": 0,
    "metadata": {
      "foo": "bar"
    },
    "preserve_on_migration": true,
    "project_id": "project_id",
    "read_only": true,
    "tags": [
      "string"
    ],
    "template_id": "template_id",
    "template_name": "template_name"
  }
]
```
