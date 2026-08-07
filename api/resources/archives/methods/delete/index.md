## Delete Archive

**delete** `/v1/archives/{archive_id}`

Delete an archive by its ID.

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/archives/$ARCHIVE_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```
