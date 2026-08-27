## Create template (Cloud-only)

**post** `/v1/templates`

Creates a new template from an existing agent or agent file

### Body Parameters

- `body: object { agent_id, type, name }  or object { agent_file, type, name, update_existing_tools }`

  The type of template to create, currently only agent templates are supported

  - `Agent object { agent_id, type, name }`

    Create a template from an existing agent

    - `agent_id: string`

      The ID of the agent to use as a template, can be from any project

    - `type: "agent"`

      - `"agent"`

    - `name: optional string`

      Optional custom name for the template. If not provided, a random name will be generated.

  - `AgentFile object { agent_file, type, name, update_existing_tools }`

    Create a template from an uploaded agent file

    - `agent_file: map[unknown]`

      The agent file to use as a template, this should be a JSON file exported from the platform

    - `type: "agent_file"`

      - `"agent_file"`

    - `name: optional string`

      Optional custom name for the template. If not provided, a random name will be generated.

    - `update_existing_tools: optional boolean`

      If true, update existing custom tools source_code and json_schema (source_type cannot be changed)

### Returns

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

- `description: optional string`

### Example

```http
curl https://api.letta.com/v1/templates \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "agent_id": "agent_id",
          "type": "agent"
        }'
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
