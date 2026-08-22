## List Embedding Models

`client.models.embeddings.list(RequestOptionsoptions?): EmbeddingListResponse`

**get** `/v1/models/embedding`

List available embedding models using the asynchronous implementation for improved performance.

Returns EmbeddingModel format which extends EmbeddingConfig with additional metadata fields.
Legacy EmbeddingConfig fields are marked as deprecated but still available for backward compatibility.

### Returns

- `EmbeddingListResponse = Array<EmbeddingModel>`

  - `display_name: string`

    Display name for the model shown in UI

  - `embedding_dim: number`

    The dimension of the embedding

  - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

    Deprecated: Use 'provider_type' field instead. The endpoint type for the embedding model.

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

    Deprecated: Use 'name' field instead. Embedding model name.

  - `name: string`

    The actual model name used by the provider

  - `provider_name: string`

    The name of the provider

  - `provider_type: ProviderType`

    The type of the provider

    - `"anthropic"`

    - `"azure"`

    - `"baseten"`

    - `"bedrock"`

    - `"cerebras"`

    - `"chatgpt_oauth"`

    - `"deepseek"`

    - `"fireworks"`

    - `"google_ai"`

    - `"google_vertex"`

    - `"groq"`

    - `"hugging-face"`

    - `"letta"`

    - `"lmstudio_openai"`

    - `"minimax"`

    - `"moonshot"`

    - `"moonshot_coding"`

    - `"mistral"`

    - `"ollama"`

    - `"openai"`

    - `"together"`

    - `"vllm"`

    - `"sglang"`

    - `"openrouter"`

    - `"xai"`

    - `"zai"`

    - `"zai_coding"`

  - `azure_deployment?: string | null`

    Deprecated: The Azure deployment for the model.

  - `azure_endpoint?: string | null`

    Deprecated: The Azure endpoint for the model.

  - `azure_version?: string | null`

    Deprecated: The Azure version for the model.

  - `batch_size?: number`

    Deprecated: The maximum batch size for processing embeddings.

  - `embedding_chunk_size?: number | null`

    Deprecated: The chunk size of the embedding.

  - `embedding_endpoint?: string | null`

    Deprecated: The endpoint for the model.

  - `handle?: string | null`

    The handle for this config, in the format provider/model-name.

  - `model_type?: "embedding"`

    Type of model (llm or embedding)

    - `"embedding"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const embeddingModels = await client.models.embeddings.list();

console.log(embeddingModels);
```

#### Response

```json
[
  {
    "display_name": "display_name",
    "embedding_dim": 0,
    "embedding_endpoint_type": "openai",
    "embedding_model": "embedding_model",
    "name": "name",
    "provider_name": "provider_name",
    "provider_type": "anthropic",
    "azure_deployment": "azure_deployment",
    "azure_endpoint": "azure_endpoint",
    "azure_version": "azure_version",
    "batch_size": 0,
    "embedding_chunk_size": 0,
    "embedding_endpoint": "embedding_endpoint",
    "handle": "handle",
    "model_type": "embedding"
  }
]
```
