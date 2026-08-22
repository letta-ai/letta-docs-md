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
