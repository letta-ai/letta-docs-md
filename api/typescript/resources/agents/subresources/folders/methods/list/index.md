## List Folders For Agent

`client.agents.folders.list(stringagentID, FolderListParamsquery?, RequestOptionsoptions?): ArrayPage<FolderListResponse>`

**get** `/v1/agents/{agent_id}/folders`

Get the folders associated with an agent.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `query: FolderListParams`

  - `after?: string | null`

    Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

  - `limit?: number | null`

    Maximum number of sources to return

  - `order?: "asc" | "desc"`

    Sort order for sources by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `FolderListResponse`

  (Deprecated: Use Folder) Representation of a source, which is a collection of files and passages.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the source.

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

  - `name: string`

    The name of the source.

  - `created_at?: string | null`

    The timestamp when the source was created.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `description?: string | null`

    The description of the source.

  - `instructions?: string | null`

    Instructions for how to use the source.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the source.

  - `updated_at?: string | null`

    The timestamp when the source was last updated.

  - `vector_db_provider?: VectorDBProvider`

    The vector database provider used for this source's passages

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
for await (const folderListResponse of client.agents.folders.list(
  'agent-123e4567-e89b-42d3-8456-426614174000',
)) {
  console.log(folderListResponse.id);
}
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
