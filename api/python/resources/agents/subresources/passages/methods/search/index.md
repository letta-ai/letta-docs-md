## Search Archival Memory

`agents.passages.search(stragent_id, PassageSearchParams**kwargs)  -> PassageSearchResponse`

**get** `/v1/agents/{agent_id}/archival-memory/search`

Search archival memory using semantic (embedding-based) search with optional temporal filtering.

This endpoint allows manual triggering of archival memory searches, enabling users to query
an agent's archival memory store directly via the API. The search uses the same functionality
as the agent's archival_memory_search tool but is accessible for external API usage.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `query: str`

  String to search for using semantic similarity

- `end_datetime: Optional[Union[str, datetime, null]]`

  Filter results to passages created before this datetime

- `start_datetime: Optional[Union[str, datetime, null]]`

  Filter results to passages created after this datetime

- `tag_match_mode: Optional[Literal["any", "all"]]`

  How to match tags - 'any' to match passages with any of the tags, 'all' to match only passages with all tags

  - `"any"`

  - `"all"`

- `tags: Optional[Sequence[str]]`

  Optional list of tags to filter search results

- `top_k: Optional[int]`

  Maximum number of results to return. Uses system default if not specified

### Returns

- `class PassageSearchResponse: …`

  - `count: int`

    Total number of results returned

  - `results: List[Result]`

    List of search results matching the query

    - `id: str`

      Unique identifier of the archival memory passage

    - `content: str`

      Text content of the archival memory passage

    - `timestamp: str`

      Timestamp of when the memory was created, formatted in agent's timezone

    - `tags: Optional[List[str]]`

      List of tags associated with this memory

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.agents.passages.search(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
    query="query",
)
print(response.count)
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
