## Search Passages

**post** `/v1/passages/search`

Search passages across the organization with optional agent and archive filtering.
Returns passages with relevance scores.

This endpoint supports semantic search through passages:

- If neither agent_id nor archive_id is provided, searches ALL passages in the organization
- If agent_id is provided, searches passages across all archives attached to that agent
- If archive_id is provided, searches passages within that specific archive
- If both are provided, agent_id takes precedence

### Body Parameters

- `agent_id: optional string`

  Filter passages by agent ID

- `archive_id: optional string`

  Filter passages by archive ID

- `end_date: optional string`

  Filter results to passages created before this datetime

- `limit: optional number`

  Maximum number of results to return

- `query: optional string`

  Text query for semantic search

- `start_date: optional string`

  Filter results to passages created after this datetime

- `tag_match_mode: optional "any" or "all"`

  How to match tags - 'any' to match passages with any of the tags, 'all' to match only passages with all tags

  - `"any"`

  - `"all"`

- `tags: optional array of string`

  Optional list of tags to filter search results

### Returns

- `passage: Passage`

  The passage object

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

- `score: number`

  Relevance score

- `metadata: optional map[unknown]`

  Additional metadata about the search result

### Example

```http
curl https://api.letta.com/v1/passages/search \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
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
