## Delete Block

**delete** `/v1/blocks/{block_id}`

Delete Block

### Path Parameters

- `block_id: string`

  The ID of the block in the format 'block-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/blocks/$BLOCK_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
