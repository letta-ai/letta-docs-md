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
