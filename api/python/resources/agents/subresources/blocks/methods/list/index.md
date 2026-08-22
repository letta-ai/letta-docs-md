## List Blocks For Agent

`agents.blocks.list(stragent_id, BlockListParams**kwargs)  -> SyncArrayPage[BlockResponse]`

**get** `/v1/agents/{agent_id}/core-memory/blocks`

Retrieve the core memory blocks of a specific agent.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `after: Optional[str]`

  Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

- `limit: Optional[int]`

  Maximum number of blocks to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for blocks by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

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
page = client.agents.blocks.list(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
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
