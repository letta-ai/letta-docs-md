# Templates

## Create template (Cloud-only)

`templates.create(TemplateCreateParams**kwargs)  -> TemplateCreateResponse`

**post** `/v1/templates`

Creates a new template from an existing agent or agent file

### Parameters

- `agent_id: str`

  The ID of the agent to use as a template, can be from any project

- `type: Literal["agent"]`

  - `"agent"`

- `name: Optional[str]`

  Optional custom name for the template. If not provided, a random name will be generated.

### Returns

- `class TemplateCreateResponse: …`

  - `id: str`

  - `latest_version: str`

    The latest version of the template

  - `name: str`

    The exact name of the template

  - `project_id: str`

  - `project_slug: str`

  - `template_deployment_slug: str`

    The full name of the template, including version and project slug

  - `updated_at: str`

    When the template was last updated

  - `description: Optional[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
template = client.templates.create(
    agent_id="agent_id",
    type="agent",
)
print(template.id)
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

`templates.save(strtemplate_name, TemplateSaveParams**kwargs)  -> TemplateSaveResponse`

**post** `/v1/templates/{template_name}/save`

Saves the current version of the template as a new version

### Parameters

- `template_name: str`

- `block_reconciliation_strategy: Optional[Literal["reconcile-all", "preserve-deleted"]]`

  Strategy for reconciling memory blocks during migration: "reconcile-all" deletes blocks not in the template, "preserve-deleted" keeps them. Defaults to "preserve-deleted".

  - `"reconcile-all"`

  - `"preserve-deleted"`

- `message: Optional[str]`

  A message to describe the changes made in this template version

- `migrate_agents: Optional[bool]`

  If true, existing agents attached to this template will be migrated to the new template version

- `preserve_core_memories_on_migration: Optional[bool]`

  If true, the core memories will be preserved in the template version when migrating agents

- `preserve_environment_variables_on_migration: Optional[bool]`

  If true, the environment variables will be preserved in the template version when migrating agents

- `preserve_sources_on_migration: Optional[bool]`

  If true, existing agent folders/sources will be preserved and merged with template sources during migration. If false, agent sources will be replaced with template sources.

### Returns

- `class TemplateSaveResponse: …`

  - `id: str`

  - `latest_version: str`

    The latest version of the template

  - `name: str`

    The exact name of the template

  - `project_id: str`

  - `project_slug: str`

  - `template_deployment_slug: str`

    The full name of the template, including version and project slug

  - `updated_at: str`

    When the template was last updated

  - `description: Optional[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.templates.save(
    template_name="template_name",
)
print(response.id)
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

`templates.delete(strtemplate_name)  -> TemplateDeleteResponse`

**delete** `/v1/templates/{template_name}`

Deletes all versions of a template with the specified name

### Parameters

- `template_name: str`

### Returns

- `class TemplateDeleteResponse: …`

  - `success: bool`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
template = client.templates.delete(
    "template_name",
)
print(template.success)
```

#### Response

```json
{
  "success": true
}
```

## Update current template from agent file (Cloud-only)

`templates.update(strtemplate_name, TemplateUpdateParams**kwargs)  -> TemplateUpdateResponse`

**patch** `/v1/templates/{template_name}`

Updates the current working version of a template from an agent file

### Parameters

- `template_name: str`

- `agent_file_json: Dict[str, Optional[object]]`

  The agent file to update the current template version from

- `save_existing_changes: Optional[bool]`

  If true, Letta will automatically save any changes as a version before updating the template

- `update_existing_tools: Optional[bool]`

  If true, update existing custom tools source_code and json_schema (source_type cannot be changed)

### Returns

- `class TemplateUpdateResponse: …`

  - `success: bool`

  - `message: Optional[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
template = client.templates.update(
    template_name="template_name",
    agent_file_json={
        "foo": "bar"
    },
)
print(template.success)
```

#### Response

```json
{
  "success": true,
  "message": "message"
}
```

## Rollback template to previous version (Cloud-only)

`templates.rollback(strtemplate_name, TemplateRollbackParams**kwargs)  -> TemplateRollbackResponse`

**post** `/v1/templates/{template_name}/rollback`

Rollback the current working version of a template to a previous saved version. If the current version has unsaved changes, they will be automatically saved as a new version before rollback.

### Parameters

- `template_name: str`

- `version: str`

  The target version to rollback to (e.g., "1", "2", "latest"). Cannot be "current" or "dev".

### Returns

- `class TemplateRollbackResponse: …`

  - `success: bool`

  - `message: Optional[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.templates.rollback(
    template_name="template_name",
    version="version",
)
print(response.success)
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

- `class TemplateCreateResponse: …`

  - `id: str`

  - `latest_version: str`

    The latest version of the template

  - `name: str`

    The exact name of the template

  - `project_id: str`

  - `project_slug: str`

  - `template_deployment_slug: str`

    The full name of the template, including version and project slug

  - `updated_at: str`

    When the template was last updated

  - `description: Optional[str]`

### Template Save Response

- `class TemplateSaveResponse: …`

  - `id: str`

  - `latest_version: str`

    The latest version of the template

  - `name: str`

    The exact name of the template

  - `project_id: str`

  - `project_slug: str`

  - `template_deployment_slug: str`

    The full name of the template, including version and project slug

  - `updated_at: str`

    When the template was last updated

  - `description: Optional[str]`

### Template Delete Response

- `class TemplateDeleteResponse: …`

  - `success: bool`

### Template Update Response

- `class TemplateUpdateResponse: …`

  - `success: bool`

  - `message: Optional[str]`

### Template Rollback Response

- `class TemplateRollbackResponse: …`

  - `success: bool`

  - `message: Optional[str]`

# Agents

## Create Agents From Template

`templates.agents.create(strtemplate_version, AgentCreateParams**kwargs)  -> AgentCreateResponse`

**post** `/v1/templates/{template_version}/agents`

Creates an Agent or multiple Agents from a template

### Parameters

- `template_version: str`

- `agent_name: Optional[str]`

  The name of the agent, optional otherwise a random one will be assigned

- `identity_ids: Optional[Sequence[str]]`

  The identity ids to assign to the agent

- `initial_message_sequence: Optional[Iterable[InitialMessageSequence]]`

  Set an initial sequence of messages, if not provided, the agent will start with the default message sequence, if an empty array is provided, the agent will start with no messages

  - `content: str`

  - `role: Literal["user", "system", "assistant"]`

    - `"user"`

    - `"system"`

    - `"assistant"`

  - `batch_item_id: Optional[str]`

  - `group_id: Optional[str]`

  - `name: Optional[str]`

  - `otid: Optional[str]`

  - `sender_id: Optional[str]`

- `memory_variables: Optional[Dict[str, str]]`

  The memory variables to assign to the agent

- `tags: Optional[Sequence[str]]`

  The tags to assign to the agent

- `tool_variables: Optional[Dict[str, str]]`

  The tool variables to assign to the agent

### Returns

- `class AgentCreateResponse: …`

  Response containing created agent IDs and associated metadata

  - `agent_ids: List[str]`

    Array of created agent IDs

  - `deployment_id: str`

    The deployment ID for the created agents

  - `group_id: Optional[str]`

    Optional group ID if agents were created in a group

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
agent = client.templates.agents.create(
    template_version="template_version",
)
print(agent.agent_ids)
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

- `class AgentCreateResponse: …`

  Response containing created agent IDs and associated metadata

  - `agent_ids: List[str]`

    Array of created agent IDs

  - `deployment_id: str`

    The deployment ID for the created agents

  - `group_id: Optional[str]`

    Optional group ID if agents were created in a group
