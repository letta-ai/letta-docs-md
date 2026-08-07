## Retrieve Block For Agent

`client.agents.blocks.retrieve(stringblockLabel, BlockRetrieveParamsparams, RequestOptionsoptions?): BlockResponse`

**get** `/v1/agents/{agent_id}/core-memory/blocks/{block_label}`

Retrieve a core memory block from an agent.

### Parameters

- `blockLabel: string`

- `params: BlockRetrieveParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

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

const blockResponse = await client.agents.blocks.retrieve('block_label', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(blockResponse.id);
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
