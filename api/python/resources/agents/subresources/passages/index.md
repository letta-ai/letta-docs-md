# Passages

## List Passages

`agents.passages.list(stragent_id, PassageListParams**kwargs)  -> PassageListResponse`

**get** `/v1/agents/{agent_id}/archival-memory`

Retrieve the memories in an agent's archival memory store (paginated query).

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `after: Optional[str]`

  Unique ID of the memory to start the query range at.

- `ascending: Optional[bool]`

  Whether to sort passages oldest to newest (True, default) or newest to oldest (False)

- `before: Optional[str]`

  Unique ID of the memory to end the query range at.

- `limit: Optional[int]`

  How many results to include in the response.

- `search: Optional[str]`

  Search passages by text

### Returns

- `List[Passage]`

  - `embedding: Optional[List[float]]`

    The embedding of the passage.

  - `embedding_config: Optional[EmbeddingConfig]`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: int`

      The dimension of the embedding.

    - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

      The endpoint type for the model.

      - `"openai"`

      - `"anthropic"`

      - `"bedrock"`

      - `"google_ai"`

      - `"google_vertex"`

      - `"azure"`

      - `"groq"`

      - `"ollama"`

      - `"webui"`

      - `"webui-legacy"`

      - `"lmstudio"`

      - `"lmstudio-legacy"`

      - `"llamacpp"`

      - `"koboldcpp"`

      - `"vllm"`

      - `"hugging-face"`

      - `"mistral"`

      - `"together"`

      - `"pinecone"`

    - `embedding_model: str`

      The model for the embedding.

    - `azure_deployment: Optional[str]`

      The Azure deployment for the model.

    - `azure_endpoint: Optional[str]`

      The Azure endpoint for the model.

    - `azure_version: Optional[str]`

      The Azure version for the model.

    - `batch_size: Optional[int]`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size: Optional[int]`

      The chunk size of the embedding.

    - `embedding_endpoint: Optional[str]`

      The endpoint for the model (`None` if local).

    - `handle: Optional[str]`

      The handle for this config, in the format provider/model-name.

  - `text: str`

    The text of the passage.

  - `id: Optional[str]`

    The human-friendly ID of the Passage

  - `archive_id: Optional[str]`

    The unique identifier of the archive containing this passage.

  - `created_at: Optional[datetime]`

    The creation date of the passage.

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `file_id: Optional[str]`

    The unique identifier of the file associated with the passage.

  - `file_name: Optional[str]`

    The name of the file (only for source passages).

  - `is_deleted: Optional[bool]`

    Whether this passage is deleted or not.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `metadata: Optional[Dict[str, object]]`

    The metadata of the passage.

  - `source_id: Optional[str]`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags: Optional[List[str]]`

    Tags associated with this passage.

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
passages = client.agents.passages.list(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(passages)
```

#### Response

```json
[
  {
    "embedding": [
      0
    ],
    "embedding_config": {
      "embedding_dim": 0,
      "embedding_endpoint_type": "openai",
      "embedding_model": "embedding_model",
      "azure_deployment": "azure_deployment",
      "azure_endpoint": "azure_endpoint",
      "azure_version": "azure_version",
      "batch_size": 0,
      "embedding_chunk_size": 0,
      "embedding_endpoint": "embedding_endpoint",
      "handle": "handle"
    },
    "text": "text",
    "id": "passage-123e4567-e89b-12d3-a456-426614174000",
    "archive_id": "archive_id",
    "created_at": "2019-12-27T18:11:19.117Z",
    "created_by_id": "created_by_id",
    "file_id": "file_id",
    "file_name": "file_name",
    "is_deleted": true,
    "last_updated_by_id": "last_updated_by_id",
    "metadata": {
      "foo": "bar"
    },
    "source_id": "source_id",
    "tags": [
      "string"
    ],
    "updated_at": "2019-12-27T18:11:19.117Z"
  }
]
```

## Create Passage

`agents.passages.create(stragent_id, PassageCreateParams**kwargs)  -> PassageCreateResponse`

**post** `/v1/agents/{agent_id}/archival-memory`

Insert a memory into an agent's archival memory store.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `text: str`

  Text to write to archival memory.

- `created_at: Optional[Union[str, datetime, null]]`

  Optional timestamp for the memory (defaults to current UTC time).

- `tags: Optional[Sequence[str]]`

  Optional list of tags to attach to the memory.

### Returns

- `List[Passage]`

  - `embedding: Optional[List[float]]`

    The embedding of the passage.

  - `embedding_config: Optional[EmbeddingConfig]`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: int`

      The dimension of the embedding.

    - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

      The endpoint type for the model.

      - `"openai"`

      - `"anthropic"`

      - `"bedrock"`

      - `"google_ai"`

      - `"google_vertex"`

      - `"azure"`

      - `"groq"`

      - `"ollama"`

      - `"webui"`

      - `"webui-legacy"`

      - `"lmstudio"`

      - `"lmstudio-legacy"`

      - `"llamacpp"`

      - `"koboldcpp"`

      - `"vllm"`

      - `"hugging-face"`

      - `"mistral"`

      - `"together"`

      - `"pinecone"`

    - `embedding_model: str`

      The model for the embedding.

    - `azure_deployment: Optional[str]`

      The Azure deployment for the model.

    - `azure_endpoint: Optional[str]`

      The Azure endpoint for the model.

    - `azure_version: Optional[str]`

      The Azure version for the model.

    - `batch_size: Optional[int]`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size: Optional[int]`

      The chunk size of the embedding.

    - `embedding_endpoint: Optional[str]`

      The endpoint for the model (`None` if local).

    - `handle: Optional[str]`

      The handle for this config, in the format provider/model-name.

  - `text: str`

    The text of the passage.

  - `id: Optional[str]`

    The human-friendly ID of the Passage

  - `archive_id: Optional[str]`

    The unique identifier of the archive containing this passage.

  - `created_at: Optional[datetime]`

    The creation date of the passage.

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `file_id: Optional[str]`

    The unique identifier of the file associated with the passage.

  - `file_name: Optional[str]`

    The name of the file (only for source passages).

  - `is_deleted: Optional[bool]`

    Whether this passage is deleted or not.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `metadata: Optional[Dict[str, object]]`

    The metadata of the passage.

  - `source_id: Optional[str]`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags: Optional[List[str]]`

    Tags associated with this passage.

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
passages = client.agents.passages.create(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
    text="text",
)
print(passages)
```

#### Response

```json
[
  {
    "embedding": [
      0
    ],
    "embedding_config": {
      "embedding_dim": 0,
      "embedding_endpoint_type": "openai",
      "embedding_model": "embedding_model",
      "azure_deployment": "azure_deployment",
      "azure_endpoint": "azure_endpoint",
      "azure_version": "azure_version",
      "batch_size": 0,
      "embedding_chunk_size": 0,
      "embedding_endpoint": "embedding_endpoint",
      "handle": "handle"
    },
    "text": "text",
    "id": "passage-123e4567-e89b-12d3-a456-426614174000",
    "archive_id": "archive_id",
    "created_at": "2019-12-27T18:11:19.117Z",
    "created_by_id": "created_by_id",
    "file_id": "file_id",
    "file_name": "file_name",
    "is_deleted": true,
    "last_updated_by_id": "last_updated_by_id",
    "metadata": {
      "foo": "bar"
    },
    "source_id": "source_id",
    "tags": [
      "string"
    ],
    "updated_at": "2019-12-27T18:11:19.117Z"
  }
]
```

## Delete Passage

`agents.passages.delete(strmemory_id, PassageDeleteParams**kwargs)  -> object`

**delete** `/v1/agents/{agent_id}/archival-memory/{memory_id}`

Delete a memory from an agent's archival memory store.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `memory_id: str`

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
passage = client.agents.passages.delete(
    memory_id="memory_id",
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(passage)
```

#### Response

```json
{}
```

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

## Domain Types

### Passage List Response

- `List[Passage]`

  - `embedding: Optional[List[float]]`

    The embedding of the passage.

  - `embedding_config: Optional[EmbeddingConfig]`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: int`

      The dimension of the embedding.

    - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

      The endpoint type for the model.

      - `"openai"`

      - `"anthropic"`

      - `"bedrock"`

      - `"google_ai"`

      - `"google_vertex"`

      - `"azure"`

      - `"groq"`

      - `"ollama"`

      - `"webui"`

      - `"webui-legacy"`

      - `"lmstudio"`

      - `"lmstudio-legacy"`

      - `"llamacpp"`

      - `"koboldcpp"`

      - `"vllm"`

      - `"hugging-face"`

      - `"mistral"`

      - `"together"`

      - `"pinecone"`

    - `embedding_model: str`

      The model for the embedding.

    - `azure_deployment: Optional[str]`

      The Azure deployment for the model.

    - `azure_endpoint: Optional[str]`

      The Azure endpoint for the model.

    - `azure_version: Optional[str]`

      The Azure version for the model.

    - `batch_size: Optional[int]`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size: Optional[int]`

      The chunk size of the embedding.

    - `embedding_endpoint: Optional[str]`

      The endpoint for the model (`None` if local).

    - `handle: Optional[str]`

      The handle for this config, in the format provider/model-name.

  - `text: str`

    The text of the passage.

  - `id: Optional[str]`

    The human-friendly ID of the Passage

  - `archive_id: Optional[str]`

    The unique identifier of the archive containing this passage.

  - `created_at: Optional[datetime]`

    The creation date of the passage.

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `file_id: Optional[str]`

    The unique identifier of the file associated with the passage.

  - `file_name: Optional[str]`

    The name of the file (only for source passages).

  - `is_deleted: Optional[bool]`

    Whether this passage is deleted or not.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `metadata: Optional[Dict[str, object]]`

    The metadata of the passage.

  - `source_id: Optional[str]`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags: Optional[List[str]]`

    Tags associated with this passage.

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

### Passage Create Response

- `List[Passage]`

  - `embedding: Optional[List[float]]`

    The embedding of the passage.

  - `embedding_config: Optional[EmbeddingConfig]`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: int`

      The dimension of the embedding.

    - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

      The endpoint type for the model.

      - `"openai"`

      - `"anthropic"`

      - `"bedrock"`

      - `"google_ai"`

      - `"google_vertex"`

      - `"azure"`

      - `"groq"`

      - `"ollama"`

      - `"webui"`

      - `"webui-legacy"`

      - `"lmstudio"`

      - `"lmstudio-legacy"`

      - `"llamacpp"`

      - `"koboldcpp"`

      - `"vllm"`

      - `"hugging-face"`

      - `"mistral"`

      - `"together"`

      - `"pinecone"`

    - `embedding_model: str`

      The model for the embedding.

    - `azure_deployment: Optional[str]`

      The Azure deployment for the model.

    - `azure_endpoint: Optional[str]`

      The Azure endpoint for the model.

    - `azure_version: Optional[str]`

      The Azure version for the model.

    - `batch_size: Optional[int]`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size: Optional[int]`

      The chunk size of the embedding.

    - `embedding_endpoint: Optional[str]`

      The endpoint for the model (`None` if local).

    - `handle: Optional[str]`

      The handle for this config, in the format provider/model-name.

  - `text: str`

    The text of the passage.

  - `id: Optional[str]`

    The human-friendly ID of the Passage

  - `archive_id: Optional[str]`

    The unique identifier of the archive containing this passage.

  - `created_at: Optional[datetime]`

    The creation date of the passage.

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `file_id: Optional[str]`

    The unique identifier of the file associated with the passage.

  - `file_name: Optional[str]`

    The name of the file (only for source passages).

  - `is_deleted: Optional[bool]`

    Whether this passage is deleted or not.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `metadata: Optional[Dict[str, object]]`

    The metadata of the passage.

  - `source_id: Optional[str]`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags: Optional[List[str]]`

    Tags associated with this passage.

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

### Passage Search Response

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
