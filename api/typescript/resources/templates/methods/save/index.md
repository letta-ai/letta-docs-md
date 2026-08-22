## Save template version (Cloud-only)

`client.templates.save(stringtemplateName, TemplateSaveParamsbody?, RequestOptionsoptions?): TemplateSaveResponse`

**post** `/v1/templates/{template_name}/save`

Saves the current version of the template as a new version

### Parameters

- `templateName: string`

- `body: TemplateSaveParams`

  - `block_reconciliation_strategy?: "reconcile-all" | "preserve-deleted"`

    Strategy for reconciling memory blocks during migration: "reconcile-all" deletes blocks not in the template, "preserve-deleted" keeps them. Defaults to "preserve-deleted".

    - `"reconcile-all"`

    - `"preserve-deleted"`

  - `message?: string`

    A message to describe the changes made in this template version

  - `migrate_agents?: boolean`

    If true, existing agents attached to this template will be migrated to the new template version

  - `preserve_core_memories_on_migration?: boolean`

    If true, the core memories will be preserved in the template version when migrating agents

  - `preserve_environment_variables_on_migration?: boolean`

    If true, the environment variables will be preserved in the template version when migrating agents

  - `preserve_sources_on_migration?: boolean`

    If true, existing agent folders/sources will be preserved and merged with template sources during migration. If false, agent sources will be replaced with template sources.

### Returns

- `TemplateSaveResponse`

  - `id: string`

  - `latest_version: string`

    The latest version of the template

  - `name: string`

    The exact name of the template

  - `project_id: string`

  - `project_slug: string`

  - `template_deployment_slug: string`

    The full name of the template, including version and project slug

  - `updated_at: string`

    When the template was last updated

  - `description?: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.templates.save('template_name');

console.log(response.id);
```

#### Response

```json
{
  "id": "id",
  "latest_version": "latest_version",
  "name": "name",
  "project_id": "project_id",
  "project_slug": "project_slug",
  "template_deployment_slug": "template_deployment_slug",
  "updated_at": "updated_at",
  "description": "description"
}
```
