# Archives

## Create Archive

`client.archives.create(ArchiveCreateParamsbody, RequestOptionsoptions?): Archive`

**post** `/v1/archives/`

Create a new archive.

### Parameters

- `body: ArchiveCreateParams`

  - `name: string`

  - `description?: string | null`

  - `embedding?: string | null`

    Embedding model handle for the archive

  - `embedding_config?: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

### Returns

- `Archive`

  Representation of an archive - a collection of archival passages that can be shared between agents.

  - `id: string`

    The human-friendly ID of the Archive

  - `created_at: string`

    The creation date of the archive

  - `name: string`

    The name of the archive

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `description?: string | null`

    A description of the archive

  - `embedding_config?: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    Additional metadata

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

  - `vector_db_provider?: VectorDBProvider`

    The vector database provider used for this archive's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const archive = await client.archives.create({ name: 'name' });

console.log(archive.id);
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

`client.archives.list(ArchiveListParamsquery?, RequestOptionsoptions?): ArrayPage<Archive>`

**get** `/v1/archives/`

Get a list of all archives for the current organization with optional filters and pagination.

### Parameters

- `query: ArchiveListParams`

  - `after?: string | null`

    Cursor for pagination (archive ID). Returns results relative to this ID in the specified sort order. Expected format: 'archive-<uuid4>'

  - `agent_id?: string | null`

    Only archives attached to this agent ID

  - `before?: string | null`

    Cursor for pagination (archive ID). Returns results relative to this ID in the specified sort order. Expected format: 'archive-<uuid4>'

  - `limit?: number | null`

    Maximum number of archives to return

  - `name?: string | null`

    Filter by archive name (exact match)

  - `order?: "asc" | "desc"`

    Sort order for archives by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `Archive`

  Representation of an archive - a collection of archival passages that can be shared between agents.

  - `id: string`

    The human-friendly ID of the Archive

  - `created_at: string`

    The creation date of the archive

  - `name: string`

    The name of the archive

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `description?: string | null`

    A description of the archive

  - `embedding_config?: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    Additional metadata

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

  - `vector_db_provider?: VectorDBProvider`

    The vector database provider used for this archive's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const archive of client.archives.list()) {
  console.log(archive.id);
}
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

`client.archives.update(stringarchiveID, ArchiveUpdateParamsbody, RequestOptionsoptions?): Archive`

**patch** `/v1/archives/{archive_id}`

Update an existing archive's name and/or description.

### Parameters

- `archiveID: string`

  The ID of the archive in the format 'archive-<uuid4>'

- `body: ArchiveUpdateParams`

  - `description?: string | null`

  - `name?: string | null`

### Returns

- `Archive`

  Representation of an archive - a collection of archival passages that can be shared between agents.

  - `id: string`

    The human-friendly ID of the Archive

  - `created_at: string`

    The creation date of the archive

  - `name: string`

    The name of the archive

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `description?: string | null`

    A description of the archive

  - `embedding_config?: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    Additional metadata

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

  - `vector_db_provider?: VectorDBProvider`

    The vector database provider used for this archive's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const archive = await client.archives.update('archive-123e4567-e89b-42d3-8456-426614174000');

console.log(archive.id);
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

`client.archives.retrieve(stringarchiveID, RequestOptionsoptions?): Archive`

**get** `/v1/archives/{archive_id}`

Get a single archive by its ID.

### Parameters

- `archiveID: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Returns

- `Archive`

  Representation of an archive - a collection of archival passages that can be shared between agents.

  - `id: string`

    The human-friendly ID of the Archive

  - `created_at: string`

    The creation date of the archive

  - `name: string`

    The name of the archive

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `description?: string | null`

    A description of the archive

  - `embedding_config?: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    Additional metadata

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

  - `vector_db_provider?: VectorDBProvider`

    The vector database provider used for this archive's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const archive = await client.archives.retrieve('archive-123e4567-e89b-42d3-8456-426614174000');

console.log(archive.id);
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

`client.archives.delete(stringarchiveID, RequestOptionsoptions?): void`

**delete** `/v1/archives/{archive_id}`

Delete an archive by its ID.

### Parameters

- `archiveID: string`

  The ID of the archive in the format 'archive-<uuid4>'

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

await client.archives.delete('archive-123e4567-e89b-42d3-8456-426614174000');
```

## Domain Types

### Archive

- `Archive`

  Representation of an archive - a collection of archival passages that can be shared between agents.

  - `id: string`

    The human-friendly ID of the Archive

  - `created_at: string`

    The creation date of the archive

  - `name: string`

    The name of the archive

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `description?: string | null`

    A description of the archive

  - `embedding_config?: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    Additional metadata

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

  - `vector_db_provider?: VectorDBProvider`

    The vector database provider used for this archive's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

### Vector DB Provider

- `VectorDBProvider = "native" | "tpuf" | "pinecone"`

  Supported vector database providers for archival memory

  - `"native"`

  - `"tpuf"`

  - `"pinecone"`

# Passages

## Create Passage In Archive

`client.archives.passages.create(stringarchiveID, PassageCreateParamsbody, RequestOptionsoptions?): Passage`

**post** `/v1/archives/{archive_id}/passages`

Create a new passage in an archive.

This adds a passage to the archive and creates embeddings for vector storage.

### Parameters

- `archiveID: string`

  The ID of the archive in the format 'archive-<uuid4>'

- `body: PassageCreateParams`

  - `text: string`

    The text content of the passage

  - `created_at?: string | null`

    Optional creation datetime for the passage (ISO 8601 format)

  - `metadata?: Record<string, unknown> | null`

    Optional metadata for the passage

  - `tags?: Array<string> | null`

    Optional tags for categorizing the passage

### Returns

- `Passage`

  Representation of a passage, which is stored in archival memory.

  - `embedding: Array<number> | null`

    The embedding of the passage.

  - `embedding_config: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `text: string`

    The text of the passage.

  - `id?: string`

    The human-friendly ID of the Passage

  - `archive_id?: string | null`

    The unique identifier of the archive containing this passage.

  - `created_at?: string | null`

    The creation date of the passage.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `file_id?: string | null`

    The unique identifier of the file associated with the passage.

  - `file_name?: string | null`

    The name of the file (only for source passages).

  - `is_deleted?: boolean`

    Whether this passage is deleted or not.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    The metadata of the passage.

  - `source_id?: string | null`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags?: Array<string> | null`

    Tags associated with this passage.

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const passage = await client.archives.passages.create(
  'archive-123e4567-e89b-42d3-8456-426614174000',
  { text: 'text' },
);

console.log(passage.id);
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

`client.archives.passages.createMany(stringarchiveID, PassageCreateManyParamsbody, RequestOptionsoptions?): PassageCreateManyResponse`

**post** `/v1/archives/{archive_id}/passages/batch`

Create multiple passages in an archive.

This adds passages to the archive and creates embeddings for vector storage.

### Parameters

- `archiveID: string`

  The ID of the archive in the format 'archive-<uuid4>'

- `body: PassageCreateManyParams`

  - `passages: Array<Passage>`

    Passages to create in the archive

    - `text: string`

      The text content of the passage

    - `created_at?: string | null`

      Optional creation datetime for the passage (ISO 8601 format)

    - `metadata?: Record<string, unknown> | null`

      Optional metadata for the passage

    - `tags?: Array<string> | null`

      Optional tags for categorizing the passage

### Returns

- `PassageCreateManyResponse = Array<Passage>`

  - `embedding: Array<number> | null`

    The embedding of the passage.

  - `embedding_config: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `text: string`

    The text of the passage.

  - `id?: string`

    The human-friendly ID of the Passage

  - `archive_id?: string | null`

    The unique identifier of the archive containing this passage.

  - `created_at?: string | null`

    The creation date of the passage.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `file_id?: string | null`

    The unique identifier of the file associated with the passage.

  - `file_name?: string | null`

    The name of the file (only for source passages).

  - `is_deleted?: boolean`

    Whether this passage is deleted or not.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    The metadata of the passage.

  - `source_id?: string | null`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags?: Array<string> | null`

    Tags associated with this passage.

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const passages = await client.archives.passages.createMany(
  'archive-123e4567-e89b-42d3-8456-426614174000',
  { passages: [{ text: 'text' }] },
);

console.log(passages);
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

`client.archives.passages.delete(stringpassageID, PassageDeleteParamsparams, RequestOptionsoptions?): void`

**delete** `/v1/archives/{archive_id}/passages/{passage_id}`

Delete a passage from an archive.

This permanently removes the passage from both the database and vector storage (if applicable).

### Parameters

- `passageID: string`

  The ID of the passage in the format 'passage-<uuid4>'

- `params: PassageDeleteParams`

  - `archive_id: string`

    The ID of the archive in the format 'archive-<uuid4>'

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

await client.archives.passages.delete('passage-123e4567-e89b-42d3-8456-426614174000', {
  archive_id: 'archive-123e4567-e89b-42d3-8456-426614174000',
});
```

## Domain Types

### Passage Create Many Response

- `PassageCreateManyResponse = Array<Passage>`

  - `embedding: Array<number> | null`

    The embedding of the passage.

  - `embedding_config: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `text: string`

    The text of the passage.

  - `id?: string`

    The human-friendly ID of the Passage

  - `archive_id?: string | null`

    The unique identifier of the archive containing this passage.

  - `created_at?: string | null`

    The creation date of the passage.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `file_id?: string | null`

    The unique identifier of the file associated with the passage.

  - `file_name?: string | null`

    The name of the file (only for source passages).

  - `is_deleted?: boolean`

    Whether this passage is deleted or not.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    The metadata of the passage.

  - `source_id?: string | null`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags?: Array<string> | null`

    Tags associated with this passage.

  - `updated_at?: string | null`

    The timestamp when the object was last updated.
