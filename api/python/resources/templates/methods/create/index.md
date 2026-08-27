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
