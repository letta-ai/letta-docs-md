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
