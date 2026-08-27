## Delete Tool

**delete** `/v1/tools/{tool_id}`

Delete a tool by name

### Path Parameters

- `tool_id: string`

  The ID of the tool in the format 'tool-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/tools/$TOOL_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
