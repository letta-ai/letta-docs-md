## Delete Passage From Archive

**delete** `/v1/archives/{archive_id}/passages/{passage_id}`

Delete a passage from an archive.

This permanently removes the passage from both the database and vector storage (if applicable).

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

- `passage_id: string`

  The ID of the passage in the format 'passage-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/archives/$ARCHIVE_ID/passages/$PASSAGE_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```
