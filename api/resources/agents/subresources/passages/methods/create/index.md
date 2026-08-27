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
