## Update Folder

`client.folders.update(stringfolderID, FolderUpdateParamsbody, RequestOptionsoptions?): Folder`

**patch** `/v1/folders/{folder_id}`

Update the name or documentation of an existing data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `body: FolderUpdateParams`

  - `description?: string | null`

    The description of the source.

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

  - `instructions?: string | null`

    Instructions for how to use the source.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the source.

  - `name?: string | null`

    The name of the source.

### Returns

- `Folder`

  Representation of a folder, which is a collection of files and passages.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

    The name of the folder.

  - `created_at?: string | null`

    The timestamp when the folder was created.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `description?: string | null`

    The description of the folder.

  - `instructions?: string | null`

    Instructions for how to use the folder.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the folder.

  - `updated_at?: string | null`

    The timestamp when the folder was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const folder = await client.folders.update('source-123e4567-e89b-42d3-8456-426614174000');

console.log(folder.id);
```

#### Response

```json
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
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```
