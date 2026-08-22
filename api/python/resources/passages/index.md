# Passages

## Search Passages

`passages.search(PassageSearchParams**kwargs)  -> PassageSearchResponse`

**post** `/v1/passages/search`

Search passages across the organization with optional agent and archive filtering.
Returns passages with relevance scores.

This endpoint supports semantic search through passages:

- If neither agent_id nor archive_id is provided, searches ALL passages in the organization
- If agent_id is provided, searches passages across all archives attached to that agent
- If archive_id is provided, searches passages within that specific archive
- If both are provided, agent_id takes precedence

### Parameters

- `agent_id: Optional[str]`

  Filter passages by agent ID

- `archive_id: Optional[str]`

  Filter passages by archive ID

- `end_date: Optional[Union[str, datetime, null]]`

  Filter results to passages created before this datetime

- `limit: Optional[int]`

  Maximum number of results to return

- `query: Optional[str]`

  Text query for semantic search

- `start_date: Optional[Union[str, datetime, null]]`

  Filter results to passages created after this datetime

- `tag_match_mode: Optional[Literal["any", "all"]]`

  How to match tags - 'any' to match passages with any of the tags, 'all' to match only passages with all tags

  - `"any"`

  - `"all"`

- `tags: Optional[Sequence[str]]`

  Optional list of tags to filter search results

### Returns

- `List[PassageSearchResponseItem]`

  - `passage: Passage`

    The passage object

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

  - `score: float`

    Relevance score

  - `metadata: Optional[Dict[str, object]]`

    Additional metadata about the search result

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.passages.search()
print(response)
```

#### Response

```json
[
  {
    "passage": {
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
    },
    "score": 0,
    "metadata": {
      "foo": "bar"
    }
  }
]
```

## Domain Types

### Passage

- `class Passage: …`

  Representation of a passage, which is stored in archival memory.

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

- `List[PassageSearchResponseItem]`

  - `passage: Passage`

    The passage object

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

  - `score: float`

    Relevance score

  - `metadata: Optional[Dict[str, object]]`

    Additional metadata about the search result
