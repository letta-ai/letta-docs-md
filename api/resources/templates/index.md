# Templates

## Create template (Cloud-only)

**post** `/v1/templates`

Creates a new template from an existing agent or agent file

### Body Parameters

- `body: object { agent_id, type, name }  or object { agent_file, type, name, update_existing_tools }`

  The type of template to create, currently only agent templates are supported

  - `Agent object { agent_id, type, name }`

    Create a template from an existing agent

    - `agent_id: string`

      The ID of the agent to use as a template, can be from any project

    - `type: "agent"`

      - `"agent"`

    - `name: optional string`

      Optional custom name for the template. If not provided, a random name will be generated.

  - `AgentFile object { agent_file, type, name, update_existing_tools }`

    Create a template from an uploaded agent file

    - `agent_file: map[unknown]`

      The agent file to use as a template, this should be a JSON file exported from the platform

    - `type: "agent_file"`

      - `"agent_file"`

    - `name: optional string`

      Optional custom name for the template. If not provided, a random name will be generated.

    - `update_existing_tools: optional boolean`

      If true, update existing custom tools source_code and json_schema (source_type cannot be changed)

### Returns

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

- `description: optional string`

### Example

```http
curl https://api.letta.com/v1/templates \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "agent_id": "agent_id",
          "type": "agent"
        }'
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

**post** `/v1/templates/{template_name}/save`

Saves the current version of the template as a new version

### Path Parameters

- `template_name: string`

### Body Parameters

- `block_reconciliation_strategy: optional "reconcile-all" or "preserve-deleted"`

  Strategy for reconciling memory blocks during migration: "reconcile-all" deletes blocks not in the template, "preserve-deleted" keeps them. Defaults to "preserve-deleted".

  - `"reconcile-all"`

  - `"preserve-deleted"`

- `message: optional string`

  A message to describe the changes made in this template version

- `migrate_agents: optional boolean`

  If true, existing agents attached to this template will be migrated to the new template version

- `preserve_core_memories_on_migration: optional boolean`

  If true, the core memories will be preserved in the template version when migrating agents

- `preserve_environment_variables_on_migration: optional boolean`

  If true, the environment variables will be preserved in the template version when migrating agents

- `preserve_sources_on_migration: optional boolean`

  If true, existing agent folders/sources will be preserved and merged with template sources during migration. If false, agent sources will be replaced with template sources.

### Returns

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

- `description: optional string`

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_NAME/save \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

**delete** `/v1/templates/{template_name}`

Deletes all versions of a template with the specified name

### Path Parameters

- `template_name: string`

### Returns

- `success: boolean`

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_NAME \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "success": true
}
```

## Update current template from agent file (Cloud-only)

**patch** `/v1/templates/{template_name}`

Updates the current working version of a template from an agent file

### Path Parameters

- `template_name: string`

### Body Parameters

- `agent_file_json: map[unknown]`

  The agent file to update the current template version from

- `save_existing_changes: optional boolean`

  If true, Letta will automatically save any changes as a version before updating the template

- `update_existing_tools: optional boolean`

  If true, update existing custom tools source_code and json_schema (source_type cannot be changed)

### Returns

- `success: boolean`

- `message: optional string`

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_NAME \
    -X PATCH \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "agent_file_json": {
            "foo": "bar"
          }
        }'
```

#### Response

```json
{
  "success": true,
  "message": "message"
}
```

## Rollback template to previous version (Cloud-only)

**post** `/v1/templates/{template_name}/rollback`

Rollback the current working version of a template to a previous saved version. If the current version has unsaved changes, they will be automatically saved as a new version before rollback.

### Path Parameters

- `template_name: string`

### Body Parameters

- `version: string`

  The target version to rollback to (e.g., "1", "2", "latest"). Cannot be "current" or "dev".

### Returns

- `success: boolean`

- `message: optional string`

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_NAME/rollback \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "version": "version"
        }'
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

- `TemplateCreateResponse object { id, latest_version, name, 5 more }`

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

  - `description: optional string`

### Template Save Response

- `TemplateSaveResponse object { id, latest_version, name, 5 more }`

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

  - `description: optional string`

### Template Delete Response

- `TemplateDeleteResponse object { success }`

  - `success: boolean`

### Template Update Response

- `TemplateUpdateResponse object { success, message }`

  - `success: boolean`

  - `message: optional string`

### Template Rollback Response

- `TemplateRollbackResponse object { success, message }`

  - `success: boolean`

  - `message: optional string`

# Agents

## Create Agents From Template

**post** `/v1/templates/{template_version}/agents`

Creates an Agent or multiple Agents from a template

### Path Parameters

- `template_version: string`

### Body Parameters

- `agent_name: optional string`

  The name of the agent, optional otherwise a random one will be assigned

- `identity_ids: optional array of string`

  The identity ids to assign to the agent

- `initial_message_sequence: optional array of object { content, role, batch_item_id, 4 more }`

  Set an initial sequence of messages, if not provided, the agent will start with the default message sequence, if an empty array is provided, the agent will start with no messages

  - `content: string`

  - `role: "user" or "system" or "assistant"`

    - `"user"`

    - `"system"`

    - `"assistant"`

  - `batch_item_id: optional string`

  - `group_id: optional string`

  - `name: optional string`

  - `otid: optional string`

  - `sender_id: optional string`

- `memory_variables: optional map[string]`

  The memory variables to assign to the agent

- `tags: optional array of string`

  The tags to assign to the agent

- `tool_variables: optional map[string]`

  The tool variables to assign to the agent

### Returns

- `agent_ids: array of string`

  Array of created agent IDs

- `deployment_id: string`

  The deployment ID for the created agents

- `group_id: string`

  Optional group ID if agents were created in a group

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_VERSION/agents \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

- `AgentCreateResponse object { agent_ids, deployment_id, group_id }`

  Response containing created agent IDs and associated metadata

  - `agent_ids: array of string`

    Array of created agent IDs

  - `deployment_id: string`

    The deployment ID for the created agents

  - `group_id: string`

    Optional group ID if agents were created in a group
