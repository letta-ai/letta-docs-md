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
