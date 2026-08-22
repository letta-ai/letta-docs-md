# Passages

## List Passages

**get** `/v1/agents/{agent_id}/archival-memory`

Retrieve the memories in an agent's archival memory store (paginated query).

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Query Parameters

- `after: optional string`

  Unique ID of the memory to start the query range at.

- `ascending: optional boolean`

  Whether to sort passages oldest to newest (True, default) or newest to oldest (False)

- `before: optional string`

  Unique ID of the memory to end the query range at.

- `limit: optional number`

  How many results to include in the response.

- `search: optional string`

  Search passages by text

### Returns

- `embedding: array of number`

  The embedding of the passage.

- `embedding_config: EmbeddingConfig`

  Configuration for embedding model connection and processing parameters.

  - `embedding_dim: number`

    The dimension of the embedding.

  - `embedding_endpoint_type: "openai" or "anthropic" or "bedrock" or 16 more`

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

  - `embedding_model: string`

    The model for the embedding.

  - `azure_deployment: optional string`

    The Azure deployment for the model.

  - `azure_endpoint: optional string`

    The Azure endpoint for the model.

  - `azure_version: optional string`

    The Azure version for the model.

  - `batch_size: optional number`

    The maximum batch size for processing embeddings.

  - `embedding_chunk_size: optional number`

    The chunk size of the embedding.

  - `embedding_endpoint: optional string`

    The endpoint for the model (`None` if local).

  - `handle: optional string`

    The handle for this config, in the format provider/model-name.

- `text: string`

  The text of the passage.

- `id: optional string`

  The human-friendly ID of the Passage

- `archive_id: optional string`

  The unique identifier of the archive containing this passage.

- `created_at: optional string`

  The creation date of the passage.

- `created_by_id: optional string`

  The id of the user that made this object.

- `file_id: optional string`

  The unique identifier of the file associated with the passage.

- `file_name: optional string`

  The name of the file (only for source passages).

- `is_deleted: optional boolean`

  Whether this passage is deleted or not.

- `last_updated_by_id: optional string`

  The id of the user that made this object.

- `metadata: optional map[unknown]`

  The metadata of the passage.

- `source_id: optional string`

  Deprecated: Use `folder_id` field instead. The data source of the passage.

- `tags: optional array of string`

  Tags associated with this passage.

- `updated_at: optional string`

  The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archival-memory \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

**post** `/v1/agents/{agent_id}/archival-memory`

Insert a memory into an agent's archival memory store.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Body Parameters

- `text: string`

  Text to write to archival memory.

- `created_at: optional string`

  Optional timestamp for the memory (defaults to current UTC time).

- `tags: optional array of string`

  Optional list of tags to attach to the memory.

### Returns

- `embedding: array of number`

  The embedding of the passage.

- `embedding_config: EmbeddingConfig`

  Configuration for embedding model connection and processing parameters.

  - `embedding_dim: number`

    The dimension of the embedding.

  - `embedding_endpoint_type: "openai" or "anthropic" or "bedrock" or 16 more`

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

  - `embedding_model: string`

    The model for the embedding.

  - `azure_deployment: optional string`

    The Azure deployment for the model.

  - `azure_endpoint: optional string`

    The Azure endpoint for the model.

  - `azure_version: optional string`

    The Azure version for the model.

  - `batch_size: optional number`

    The maximum batch size for processing embeddings.

  - `embedding_chunk_size: optional number`

    The chunk size of the embedding.

  - `embedding_endpoint: optional string`

    The endpoint for the model (`None` if local).

  - `handle: optional string`

    The handle for this config, in the format provider/model-name.

- `text: string`

  The text of the passage.

- `id: optional string`

  The human-friendly ID of the Passage

- `archive_id: optional string`

  The unique identifier of the archive containing this passage.

- `created_at: optional string`

  The creation date of the passage.

- `created_by_id: optional string`

  The id of the user that made this object.

- `file_id: optional string`

  The unique identifier of the file associated with the passage.

- `file_name: optional string`

  The name of the file (only for source passages).

- `is_deleted: optional boolean`

  Whether this passage is deleted or not.

- `last_updated_by_id: optional string`

  The id of the user that made this object.

- `metadata: optional map[unknown]`

  The metadata of the passage.

- `source_id: optional string`

  Deprecated: Use `folder_id` field instead. The data source of the passage.

- `tags: optional array of string`

  Tags associated with this passage.

- `updated_at: optional string`

  The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archival-memory \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "text": "text"
        }'
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

**delete** `/v1/agents/{agent_id}/archival-memory/{memory_id}`

Delete a memory from an agent's archival memory store.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `memory_id: string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archival-memory/$MEMORY_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

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

## Domain Types

### Passage List Response

- `PassageListResponse = array of Passage`

  - `embedding: array of number`

    The embedding of the passage.

  - `embedding_config: EmbeddingConfig`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" or "anthropic" or "bedrock" or 16 more`

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

    - `embedding_model: string`

      The model for the embedding.

    - `azure_deployment: optional string`

      The Azure deployment for the model.

    - `azure_endpoint: optional string`

      The Azure endpoint for the model.

    - `azure_version: optional string`

      The Azure version for the model.

    - `batch_size: optional number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size: optional number`

      The chunk size of the embedding.

    - `embedding_endpoint: optional string`

      The endpoint for the model (`None` if local).

    - `handle: optional string`

      The handle for this config, in the format provider/model-name.

  - `text: string`

    The text of the passage.

  - `id: optional string`

    The human-friendly ID of the Passage

  - `archive_id: optional string`

    The unique identifier of the archive containing this passage.

  - `created_at: optional string`

    The creation date of the passage.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `file_id: optional string`

    The unique identifier of the file associated with the passage.

  - `file_name: optional string`

    The name of the file (only for source passages).

  - `is_deleted: optional boolean`

    Whether this passage is deleted or not.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `metadata: optional map[unknown]`

    The metadata of the passage.

  - `source_id: optional string`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags: optional array of string`

    Tags associated with this passage.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Passage Create Response

- `PassageCreateResponse = array of Passage`

  - `embedding: array of number`

    The embedding of the passage.

  - `embedding_config: EmbeddingConfig`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" or "anthropic" or "bedrock" or 16 more`

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

    - `embedding_model: string`

      The model for the embedding.

    - `azure_deployment: optional string`

      The Azure deployment for the model.

    - `azure_endpoint: optional string`

      The Azure endpoint for the model.

    - `azure_version: optional string`

      The Azure version for the model.

    - `batch_size: optional number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size: optional number`

      The chunk size of the embedding.

    - `embedding_endpoint: optional string`

      The endpoint for the model (`None` if local).

    - `handle: optional string`

      The handle for this config, in the format provider/model-name.

  - `text: string`

    The text of the passage.

  - `id: optional string`

    The human-friendly ID of the Passage

  - `archive_id: optional string`

    The unique identifier of the archive containing this passage.

  - `created_at: optional string`

    The creation date of the passage.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `file_id: optional string`

    The unique identifier of the file associated with the passage.

  - `file_name: optional string`

    The name of the file (only for source passages).

  - `is_deleted: optional boolean`

    Whether this passage is deleted or not.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `metadata: optional map[unknown]`

    The metadata of the passage.

  - `source_id: optional string`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags: optional array of string`

    Tags associated with this passage.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Passage Delete Response

- `PassageDeleteResponse = unknown`

### Passage Search Response

- `PassageSearchResponse object { count, results }`

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
