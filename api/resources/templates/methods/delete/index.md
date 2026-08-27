## Delete template (Cloud-only)

**delete** `/v1/templates/{template_name}`

Deletes all versions of a template with the specified name

### Path Parameters

- `template_name: string`

### Returns

- `success: boolean`

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_NAME \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "success": true
}
```
