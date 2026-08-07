# Archives

## Create Archive

**post** `/v1/archives/`

Create a new archive.

### Body Parameters

- `name: string`

- `description: optional string`

- `embedding: optional string`

  Embedding model handle for the archive

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
curl https://api.letta.com/v1/archives/ \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "name": "name"
        }'
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

## List Archives

**get** `/v1/archives/`

Get a list of all archives for the current organization with optional filters and pagination.

### Query Parameters

- `after: optional string`

  Cursor for pagination (archive ID). Returns results relative to this ID in the specified sort order. Expected format: 'archive-<uuid4>'

- `agent_id: optional string`

  Only archives attached to this agent ID

- `before: optional string`

  Cursor for pagination (archive ID). Returns results relative to this ID in the specified sort order. Expected format: 'archive-<uuid4>'

- `limit: optional number`

  Maximum number of archives to return

- `name: optional string`

  Filter by archive name (exact match)

- `order: optional "asc" or "desc"`

  Sort order for archives by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

### Returns

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
curl https://api.letta.com/v1/archives/ \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
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
]
```

## Update Archive

**patch** `/v1/archives/{archive_id}`

Update an existing archive's name and/or description.

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Body Parameters

- `description: optional string`

- `name: optional string`

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
    -X PATCH \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
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

## Delete Archive

**delete** `/v1/archives/{archive_id}`

Delete an archive by its ID.

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/archives/$ARCHIVE_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

## Domain Types

### Archive

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

### Vector DB Provider

- `VectorDBProvider = "native" or "tpuf" or "pinecone"`

  Supported vector database providers for archival memory

  - `"native"`

  - `"tpuf"`

  - `"pinecone"`

# Passages

## Create Passage In Archive

**post** `/v1/archives/{archive_id}/passages`

Create a new passage in an archive.

This adds a passage to the archive and creates embeddings for vector storage.

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Body Parameters

- `text: string`

  The text content of the passage

- `created_at: optional string`

  Optional creation datetime for the passage (ISO 8601 format)

- `metadata: optional map[unknown]`

  Optional metadata for the passage

- `tags: optional array of string`

  Optional tags for categorizing the passage

### Returns

- `Passage object { embedding, embedding_config, text, 12 more }`

  Representation of a passage, which is stored in archival memory.

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
curl https://api.letta.com/v1/archives/$ARCHIVE_ID/passages \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "text": "text"
        }'
```

#### Response

```json
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
```

## Create Passages In Archive

**post** `/v1/archives/{archive_id}/passages/batch`

Create multiple passages in an archive.

This adds passages to the archive and creates embeddings for vector storage.

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Body Parameters

- `passages: array of object { text, created_at, metadata, tags }`

  Passages to create in the archive

  - `text: string`

    The text content of the passage

  - `created_at: optional string`

    Optional creation datetime for the passage (ISO 8601 format)

  - `metadata: optional map[unknown]`

    Optional metadata for the passage

  - `tags: optional array of string`

    Optional tags for categorizing the passage

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
curl https://api.letta.com/v1/archives/$ARCHIVE_ID/passages/batch \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "passages": [
            {
              "text": "text"
            }
          ]
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

## Delete Passage From Archive

**delete** `/v1/archives/{archive_id}/passages/{passage_id}`

Delete a passage from an archive.

This permanently removes the passage from both the database and vector storage (if applicable).

### Path Parameters

- `archive_id: string`

  The ID of the archive in the format 'archive-<uuid4>'

- `passage_id: string`

  The ID of the passage in the format 'passage-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/archives/$ARCHIVE_ID/passages/$PASSAGE_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

## Domain Types

### Passage Create Many Response

- `PassageCreateManyResponse = array of Passage`

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
