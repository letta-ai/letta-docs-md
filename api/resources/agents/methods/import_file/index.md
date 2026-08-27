## Import Agent

**post** `/v1/agents/import`

Import a serialized agent file and recreate the agent(s) in the system.
Returns the IDs of all imported agents.

### Header Parameters

- `"x-override-embedding-model": optional string`

### Returns

- `agent_ids: array of string`

  List of IDs of the imported agents

### Example

```http
curl https://api.letta.com/v1/agents/import \
    -H 'Content-Type: multipart/form-data' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -F 'file=@/path/to/file'
```

#### Response

```json
{
  "agent_ids": [
    "string"
  ]
}
```
