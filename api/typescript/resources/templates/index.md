# Templates

## Create template (Cloud-only)

`client.templates.create(TemplateCreateParamsbody, RequestOptionsoptions?): TemplateCreateResponse`

**post** `/v1/templates`

Creates a new template from an existing agent or agent file

### Parameters

- `TemplateCreateParams = Variant0 | Variant1`

  - `TemplateCreateParamsBase`

    - `agent_id: string`

      The ID of the agent to use as a template, can be from any project

    - `type: "agent"`

      - `"agent"`

    - `name?: string`

      Optional custom name for the template. If not provided, a random name will be generated.

  - `Variant0 extends TemplateCreateParamsBase`

  - `Variant1 extends TemplateCreateParamsBase`

### Returns

- `TemplateCreateResponse`

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

const template = await client.templates.create({ agent_id: 'agent_id', type: 'agent' });

console.log(template.id);
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

## Delete template (Cloud-only)

`client.templates.delete(stringtemplateName, TemplateDeleteParamsbody?, RequestOptionsoptions?): TemplateDeleteResponse`

**delete** `/v1/templates/{template_name}`

Deletes all versions of a template with the specified name

### Parameters

- `templateName: string`

- `body: TemplateDeleteParams`

### Returns

- `TemplateDeleteResponse`

  - `success: boolean`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const template = await client.templates.delete('template_name');

console.log(template.success);
```

#### Response

```json
{
  "success": true
}
```

## Update current template from agent file (Cloud-only)

`client.templates.update(stringtemplateName, TemplateUpdateParamsbody, RequestOptionsoptions?): TemplateUpdateResponse`

**patch** `/v1/templates/{template_name}`

Updates the current working version of a template from an agent file

### Parameters

- `templateName: string`

- `body: TemplateUpdateParams`

  - `agent_file_json: Record<string, unknown>`

    The agent file to update the current template version from

  - `save_existing_changes?: boolean`

    If true, Letta will automatically save any changes as a version before updating the template

  - `update_existing_tools?: boolean`

    If true, update existing custom tools source_code and json_schema (source_type cannot be changed)

### Returns

- `TemplateUpdateResponse`

  - `success: boolean`

  - `message?: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const template = await client.templates.update('template_name', {
  agent_file_json: { foo: 'bar' },
});

console.log(template.success);
```

#### Response

```json
{
  "success": true,
  "message": "message"
}
```

## Rollback template to previous version (Cloud-only)

`client.templates.rollback(stringtemplateName, TemplateRollbackParamsbody, RequestOptionsoptions?): TemplateRollbackResponse`

**post** `/v1/templates/{template_name}/rollback`

Rollback the current working version of a template to a previous saved version. If the current version has unsaved changes, they will be automatically saved as a new version before rollback.

### Parameters

- `templateName: string`

- `body: TemplateRollbackParams`

  - `version: string`

    The target version to rollback to (e.g., "1", "2", "latest"). Cannot be "current" or "dev".

### Returns

- `TemplateRollbackResponse`

  - `success: boolean`

  - `message?: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.templates.rollback('template_name', { version: 'version' });

console.log(response.success);
```

#### Response

```json
{
  "success": true,
  "message": "message"
}
```

## Domain Types

### Template Create Response

- `TemplateCreateResponse`

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

### Template Save Response

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

### Template Delete Response

- `TemplateDeleteResponse`

  - `success: boolean`

### Template Update Response

- `TemplateUpdateResponse`

  - `success: boolean`

  - `message?: string`

### Template Rollback Response

- `TemplateRollbackResponse`

  - `success: boolean`

  - `message?: string`

# Agents

## Create Agents From Template

`client.templates.agents.create(stringtemplateVersion, AgentCreateParamsbody?, RequestOptionsoptions?): AgentCreateResponse`

**post** `/v1/templates/{template_version}/agents`

Creates an Agent or multiple Agents from a template

### Parameters

- `templateVersion: string`

- `body: AgentCreateParams`

  - `agent_name?: string`

    The name of the agent, optional otherwise a random one will be assigned

  - `identity_ids?: Array<string>`

    The identity ids to assign to the agent

  - `initial_message_sequence?: Array<InitialMessageSequence>`

    Set an initial sequence of messages, if not provided, the agent will start with the default message sequence, if an empty array is provided, the agent will start with no messages

    - `content: string`

    - `role: "user" | "system" | "assistant"`

      - `"user"`

      - `"system"`

      - `"assistant"`

    - `batch_item_id?: string | null`

    - `group_id?: string | null`

    - `name?: string | null`

    - `otid?: string | null`

    - `sender_id?: string | null`

  - `memory_variables?: Record<string, string>`

    The memory variables to assign to the agent

  - `tags?: Array<string>`

    The tags to assign to the agent

  - `tool_variables?: Record<string, string>`

    The tool variables to assign to the agent

### Returns

- `AgentCreateResponse`

  Response containing created agent IDs and associated metadata

  - `agent_ids: Array<string>`

    Array of created agent IDs

  - `deployment_id: string`

    The deployment ID for the created agents

  - `group_id: string | null`

    Optional group ID if agents were created in a group

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const agent = await client.templates.agents.create('template_version');

console.log(agent.agent_ids);
```

#### Response

```json
{
  "agent_ids": [
    "string"
  ],
  "deployment_id": "deployment_id",
  "group_id": "group_id"
}
```

## Domain Types

### Agent Create Response

- `AgentCreateResponse`

  Response containing created agent IDs and associated metadata

  - `agent_ids: Array<string>`

    Array of created agent IDs

  - `deployment_id: string`

    The deployment ID for the created agents

  - `group_id: string | null`

    Optional group ID if agents were created in a group
