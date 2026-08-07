## List Blocks

`client.blocks.list(BlockListParamsquery?, RequestOptionsoptions?): ArrayPage<BlockResponse>`

**get** `/v1/blocks/`

List Blocks

### Parameters

- `query: BlockListParams`

  - `after?: string | null`

    Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (block ID). Returns results relative to this ID in the specified sort order. Expected format: 'block-<uuid4>'

  - `connected_to_agents_count_eq?: Array<number> | null`

    Filter blocks by the exact number of connected agents. If provided, returns blocks that have exactly this number of connected agents.

  - `connected_to_agents_count_gt?: number | null`

    Filter blocks by the number of connected agents. If provided, returns blocks that have more than this number of connected agents.

  - `connected_to_agents_count_lt?: number | null`

    Filter blocks by the number of connected agents. If provided, returns blocks that have less than this number of connected agents.

  - `description_search?: string | null`

    Search blocks by description. If provided, returns blocks whose description matches the search query. This is a full-text search on block descriptions.

  - `identifier_keys?: Array<string> | null`

    Search agents by identifier keys

  - `identity_id?: string | null`

    The ID of the identity in the format 'identity-<uuid4>'

  - `label?: string | null`

    Label to include (alphanumeric, hyphens, underscores, forward slashes)

  - `label_search?: string | null`

    Search blocks by label. If provided, returns blocks whose label matches the search query. This is a full-text search on block labels.

  - `limit?: number | null`

    Number of blocks to return

  - `match_all_tags?: boolean`

    If True, only returns blocks that match ALL given tags. Otherwise, return blocks that have ANY of the passed-in tags.

  - `name?: string | null`

    Name filter (alphanumeric, spaces, hyphens, underscores)

  - `order?: "asc" | "desc"`

    Sort order for blocks by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

  - `project_id?: string | null`

    Search blocks by project id

  - `tags?: Array<string> | null`

    List of tags to filter blocks by

  - `templates_only?: boolean`

    Whether to include only templates

  - `value_search?: string | null`

    Search blocks by value. If provided, returns blocks whose value matches the search query. This is a full-text search on block values.

### Returns

- `BlockResponse`

  - `id: string`

    The id of the block.

  - `value: string`

    Value of the block.

  - `base_template_id?: string | null`

    (Deprecated) The base template id of the block.

  - `created_by_id?: string | null`

    The id of the user that made this Block.

  - `deployment_id?: string | null`

    (Deprecated) The id of the deployment.

  - `description?: string | null`

    Description of the block.

  - `entity_id?: string | null`

    (Deprecated) The id of the entity within the template.

  - `hidden?: boolean | null`

    (Deprecated) If set to True, the block will be hidden.

  - `is_template?: boolean`

    Whether the block is a template (e.g. saved human/persona options).

  - `label?: string | null`

    Label of the block (e.g. 'human', 'persona') in the context window.

  - `last_updated_by_id?: string | null`

    The id of the user that last updated this Block.

  - `limit?: number`

    Character limit of the block.

  - `metadata?: Record<string, unknown> | null`

    Metadata of the block.

  - `preserve_on_migration?: boolean | null`

    (Deprecated) Preserve the block on template migration.

  - `project_id?: string | null`

    The associated project id.

  - `read_only?: boolean`

    (Deprecated) Whether the agent has read-only access to the block.

  - `tags?: Array<string> | null`

    The tags associated with the block.

  - `template_id?: string | null`

    (Deprecated) The id of the template.

  - `template_name?: string | null`

    (Deprecated) The name of the block template (if it is a template).

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const blockResponse of client.blocks.list()) {
  console.log(blockResponse.id);
}
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
