## Search Archival Memory

**get** `/v1/agents/{agent_id}/archival-memory/search`

Search archival memory using semantic (embedding-based) search with optional temporal filtering.

This endpoint allows manual triggering of archival memory searches, enabling users to query
an agent's archival memory store directly via the API. The search uses the same functionality
as the agent's archival_memory_search tool but is accessible for external API usage.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Query Parameters

- `query: string`

  String to search for using semantic similarity

- `end_datetime: optional string`

  Filter results to passages created before this datetime

- `start_datetime: optional string`

  Filter results to passages created after this datetime

- `tag_match_mode: optional "any" or "all"`

  How to match tags - 'any' to match passages with any of the tags, 'all' to match only passages with all tags

  - `"any"`

  - `"all"`

- `tags: optional array of string`

  Optional list of tags to filter search results

- `top_k: optional number`

  Maximum number of results to return. Uses system default if not specified

### Returns

- `count: number`

  Total number of results returned

- `results: array of object { id, content, timestamp, tags }`

  List of search results matching the query

  - `id: string`

    Unique identifier of the archival memory passage

  - `content: string`

    Text content of the archival memory passage

  - `timestamp: string`

    Timestamp of when the memory was created, formatted in agent's timezone

  - `tags: optional array of string`

    List of tags associated with this memory

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archival-memory/search \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "count": 0,
  "results": [
    {
      "id": "id",
      "content": "content",
      "timestamp": "timestamp",
      "tags": [
        "string"
      ]
    }
  ]
}
```
