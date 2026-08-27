## Create Block

`blocks.create(BlockCreateParams**kwargs)  -> BlockResponse`

**post** `/v1/blocks/`

Create Block

### Parameters

- `label: str`

  Label of the block.

- `value: str`

  Value of the block.

- `base_template_id: Optional[str]`

  The base template id of the block.

- `deployment_id: Optional[str]`

  The id of the deployment.

- `description: Optional[str]`

  Description of the block.

- `entity_id: Optional[str]`

  The id of the entity within the template.

- `hidden: Optional[bool]`

  If set to True, the block will be hidden.

- `is_template: Optional[bool]`

- `limit: Optional[int]`

  Character limit of the block.

- `metadata: Optional[Dict[str, object]]`

  Metadata of the block.

- `preserve_on_migration: Optional[bool]`

  Preserve the block on template migration.

- `project_id: Optional[str]`

  The associated project id.

- `read_only: Optional[bool]`

  Whether the agent has read-only access to the block.

- `tags: Optional[Sequence[str]]`

  The tags to associate with the block.

- `template_id: Optional[str]`

  The id of the template.

- `template_name: Optional[str]`

  Name of the block if it is a template.

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
block_response = client.blocks.create(
    label="label",
    value="value",
)
print(block_response.id)
```

#### Response

```json
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
```
