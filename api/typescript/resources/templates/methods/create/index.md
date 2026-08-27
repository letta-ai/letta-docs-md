## Create template (Cloud-only)

`client.templates.create(TemplateCreateParamsbody, RequestOptionsoptions?): TemplateCreateResponse`

**post** `/v1/templates`

Creates a new template from an existing agent or agent file

### Parameters

- `TemplateCreateParams = Variant0 | Variant1`

  - `TemplateCreateParamsBase`

    - `agent_id: string`

      The ID of the agent to use as a template, can be from any project

    - `type: "agent"`

      - `"agent"`

    - `name?: string`

      Optional custom name for the template. If not provided, a random name will be generated.

  - `Variant0 extends TemplateCreateParamsBase`

  - `Variant1 extends TemplateCreateParamsBase`

### Returns

- `TemplateCreateResponse`

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

  - `description?: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const template = await client.templates.create({ agent_id: 'agent_id', type: 'agent' });

console.log(template.id);
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
