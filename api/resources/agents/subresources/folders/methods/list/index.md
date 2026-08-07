## List Folders For Agent

**get** `/v1/agents/{agent_id}/folders`

Get the folders associated with an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Query Parameters

- `after: optional string`

  Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

- `before: optional string`

  Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

- `limit: optional number`

  Maximum number of sources to return

- `order: optional "asc" or "desc"`

  Sort order for sources by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

### Returns

- `id: string`

  The human-friendly ID of the Source

- `embedding_config: EmbeddingConfig`

  The embedding configuration used by the source.

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

- `name: string`

  The name of the source.

- `created_at: optional string`

  The timestamp when the source was created.

- `created_by_id: optional string`

  The id of the user that made this Tool.

- `description: optional string`

  The description of the source.

- `instructions: optional string`

  Instructions for how to use the source.

- `last_updated_by_id: optional string`

  The id of the user that made this Tool.

- `metadata: optional map[unknown]`

  Metadata associated with the source.

- `updated_at: optional string`

  The timestamp when the source was last updated.

- `vector_db_provider: optional VectorDBProvider`

  The vector database provider used for this source's passages

  - `"native"`

  - `"tpuf"`

  - `"pinecone"`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/folders \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  {
    "id": "source-123e4567-e89b-12d3-a456-426614174000",
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
    "name": "name",
    "created_at": "2019-12-27T18:11:19.117Z",
    "created_by_id": "created_by_id",
    "description": "description",
    "instructions": "instructions",
    "last_updated_by_id": "last_updated_by_id",
    "metadata": {
      "foo": "bar"
    },
    "updated_at": "2019-12-27T18:11:19.117Z",
    "vector_db_provider": "native"
  }
]
```
