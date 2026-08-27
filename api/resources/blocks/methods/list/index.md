## List Blocks

**get** `/v1/blocks/`

List Blocks

### Query Parameters

- `after: optional string`

  Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

- `before: optional string`

  Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

- `connected_to_agents_count_eq: optional array of number`

  Filter blocks by the exact number of connected agents. If provided, returns blocks that have exactly this number of connected agents.

- `connected_to_agents_count_gt: optional number`

  Filter blocks by the number of connected agents. If provided, returns blocks that have more than this number of connected agents.

- `connected_to_agents_count_lt: optional number`

  Filter blocks by the number of connected agents. If provided, returns blocks that have less than this number of connected agents.

- `description_search: optional string`

  Search blocks by description. If provided, returns blocks whose description matches the search query. This is a full-text search on block descriptions.

- `identifier_keys: optional array of string`

  Search agents by identifier keys

- `identity_id: optional string`

  The ID of the identity in the format 'identity-<uuid4>'

- `label: optional string`

  Label to include (alphanumeric, hyphens, underscores, forward slashes)

- `label_search: optional string`

  Search blocks by label. If provided, returns blocks whose label matches the search query. This is a full-text search on block labels.

- `limit: optional number`

  Number of blocks to return

- `match_all_tags: optional boolean`

  If True, only returns blocks that match ALL given tags. Otherwise, return blocks that have ANY of the passed-in tags.

- `name: optional string`

  Name filter (alphanumeric, spaces, hyphens, underscores)

- `order: optional "asc" or "desc"`

  Sort order for blocks by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

- `project_id: optional string`

  Search blocks by project id

- `tags: optional array of string`

  List of tags to filter blocks by

- `templates_only: optional boolean`

  Whether to include only templates

- `value_search: optional string`

  Search blocks by value. If provided, returns blocks whose value matches the search query. This is a full-text search on block values.

### Returns

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
curl https://api.letta.com/v1/blocks/ \
    -H "Authorization: Bearer $LETTA_API_KEY"
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
