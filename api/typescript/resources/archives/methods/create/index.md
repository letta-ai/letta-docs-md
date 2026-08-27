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
