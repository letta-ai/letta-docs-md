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
