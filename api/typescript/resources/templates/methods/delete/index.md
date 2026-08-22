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
