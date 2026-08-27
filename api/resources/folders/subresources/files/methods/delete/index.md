## Delete File From Folder

**delete** `/v1/folders/{folder_id}/{file_id}`

Delete a file from a folder.

### Path Parameters

- `folder_id: string`

  The ID of the source in the format 'source-<uuid4>'

- `file_id: string`

  The ID of the file in the format 'file-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/folders/$FOLDER_ID/$FILE_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```
