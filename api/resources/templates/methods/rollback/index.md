## Rollback template to previous version (Cloud-only)

**post** `/v1/templates/{template_name}/rollback`

Rollback the current working version of a template to a previous saved version. If the current version has unsaved changes, they will be automatically saved as a new version before rollback.

### Path Parameters

- `template_name: string`

### Body Parameters

- `version: string`

  The target version to rollback to (e.g., "1", "2", "latest"). Cannot be "current" or "dev".

### Returns

- `success: boolean`

- `message: optional string`

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_NAME/rollback \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "version": "version"
        }'
```

#### Response

```json
{
  "success": true,
  "message": "message"
}
```
