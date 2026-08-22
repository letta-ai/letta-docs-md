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
