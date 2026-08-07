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
