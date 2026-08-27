## Delete Folder

**delete** `/v1/folders/{folder_id}`

Delete a data folder.

### Path Parameters

- `folder_id: string`

  The ID of the source in the format 'source-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/folders/$FOLDER_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
