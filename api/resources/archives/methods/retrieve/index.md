## Retrieve Archive

**get** `/v1/archives/{archive_id}`

Get a single archive by its ID.

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Returns

- `Archive object { id, created_at, name, 7 more }`

  Representation of an archive - a collection of archival passages that can be shared between agents.

  - `id: string`

    The human-friendly ID of the Archive

  - `created_at: string`

    The creation date of the archive

  - `name: string`

    The name of the archive

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    A description of the archive

  - `embedding_config: optional EmbeddingConfig`

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

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `metadata: optional map[unknown]`

    Additional metadata

  - `updated_at: optional string`

    The timestamp when the object was last updated.

  - `vector_db_provider: optional VectorDBProvider`

    The vector database provider used for this archive's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

### Example

```http
curl https://api.letta.com/v1/archives/$ARCHIVE_ID \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "id": "archive-123e4567-e89b-12d3-a456-426614174000",
  "created_at": "2019-12-27T18:11:19.117Z",
  "name": "name",
  "created_by_id": "created_by_id",
  "description": "description",
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
  "last_updated_by_id": "last_updated_by_id",
  "metadata": {
    "foo": "bar"
  },
  "updated_at": "2019-12-27T18:11:19.117Z",
  "vector_db_provider": "native"
}
```
