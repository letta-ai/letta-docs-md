## Update current template from agent file (Cloud-only)

**patch** `/v1/templates/{template_name}`

Updates the current working version of a template from an agent file

### Path Parameters

- `template_name: string`

### Body Parameters

- `agent_file_json: map[unknown]`

  The agent file to update the current template version from

- `save_existing_changes: optional boolean`

  If true, Letta will automatically save any changes as a version before updating the template

- `update_existing_tools: optional boolean`

  If true, update existing custom tools source_code and json_schema (source_type cannot be changed)

### Returns

- `success: boolean`

- `message: optional string`

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_NAME \
    -X PATCH \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "agent_file_json": {
            "foo": "bar"
          }
        }'
```

#### Response

```json
{
  "success": true,
  "message": "message"
}
```
