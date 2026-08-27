## Update Block

**patch** `/v1/blocks/{block_id}`

Update Block

### Path Parameters

- `block_id: string`

  The ID of the block in the format 'block-<uuid4>'

### Body Parameters

- `base_template_id: optional string`

  The base template id of the block.

- `deployment_id: optional string`

  The id of the deployment.

- `description: optional string`

  Description of the block.

- `entity_id: optional string`

  The id of the entity within the template.

- `hidden: optional boolean`

  If set to True, the block will be hidden.

- `is_template: optional boolean`

  Whether the block is a template (e.g. saved human/persona options).

- `label: optional string`

  Label of the block (e.g. 'human', 'persona') in the context window.

- `limit: optional number`

  Character limit of the block.

- `metadata: optional map[unknown]`

  Metadata of the block.

- `preserve_on_migration: optional boolean`

  Preserve the block on template migration.

- `project_id: optional string`

  The associated project id.

- `read_only: optional boolean`

  Whether the agent has read-only access to the block.

- `tags: optional array of string`

  The tags to associate with the block.

- `template_id: optional string`

  The id of the template.

- `template_name: optional string`

  Name of the block if it is a template.

- `value: optional string`

  Value of the block.

### Returns

- `BlockResponse object { id, value, base_template_id, 16 more }`

  - `id: string`

    The id of the block.

  - `value: string`

    Value of the block.

  - `base_template_id: optional string`

    (Deprecated) The base template id of the block.

  - `created_by_id: optional string`

    The id of the user that made this Block.

  - `deployment_id: optional string`

    (Deprecated) The id of the deployment.

  - `description: optional string`

    Description of the block.

  - `entity_id: optional string`

    (Deprecated) The id of the entity within the template.

  - `hidden: optional boolean`

    (Deprecated) If set to True, the block will be hidden.

  - `is_template: optional boolean`

    Whether the block is a template (e.g. saved human/persona options).

  - `label: optional string`

    Label of the block (e.g. 'human', 'persona') in the context window.

  - `last_updated_by_id: optional string`

    The id of the user that last updated this Block.

  - `limit: optional number`

    Character limit of the block.

  - `metadata: optional map[unknown]`

    Metadata of the block.

  - `preserve_on_migration: optional boolean`

    (Deprecated) Preserve the block on template migration.

  - `project_id: optional string`

    The associated project id.

  - `read_only: optional boolean`

    (Deprecated) Whether the agent has read-only access to the block.

  - `tags: optional array of string`

    The tags associated with the block.

  - `template_id: optional string`

    (Deprecated) The id of the template.

  - `template_name: optional string`

    (Deprecated) The name of the block template (if it is a template).

### Example

```http
curl https://api.letta.com/v1/blocks/$BLOCK_ID \
    -X PATCH \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
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
