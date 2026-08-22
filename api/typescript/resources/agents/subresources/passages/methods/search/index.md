## Search Archival Memory

`client.agents.passages.search(stringagentID, PassageSearchParamsquery, RequestOptionsoptions?): PassageSearchResponse`

**get** `/v1/agents/{agent_id}/archival-memory/search`

Search archival memory using semantic (embedding-based) search with optional temporal filtering.

This endpoint allows manual triggering of archival memory searches, enabling users to query
an agent's archival memory store directly via the API. The search uses the same functionality
as the agent's archival_memory_search tool but is accessible for external API usage.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `query: PassageSearchParams`

  - `query: string`

    String to search for using semantic similarity

  - `end_datetime?: string | null`

    Filter results to passages created before this datetime

  - `start_datetime?: string | null`

    Filter results to passages created after this datetime

  - `tag_match_mode?: "any" | "all"`

    How to match tags - 'any' to match passages with any of the tags, 'all' to match only passages with all tags

    - `"any"`

    - `"all"`

  - `tags?: Array<string> | null`

    Optional list of tags to filter search results

  - `top_k?: number | null`

    Maximum number of results to return. Uses system default if not specified

### Returns

- `PassageSearchResponse`

  - `count: number`

    Total number of results returned

  - `results: Array<Result>`

    List of search results matching the query

    - `id: string`

      Unique identifier of the archival memory passage

    - `content: string`

      Text content of the archival memory passage

    - `timestamp: string`

      Timestamp of when the memory was created, formatted in agent's timezone

    - `tags?: Array<string>`

      List of tags associated with this memory

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.passages.search('agent-123e4567-e89b-42d3-8456-426614174000', {
  query: 'query',
});

console.log(response.count);
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
