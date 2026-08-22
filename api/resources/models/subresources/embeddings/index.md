# Embeddings

## List Embedding Models

**get** `/v1/models/embedding`

List available embedding models using the asynchronous implementation for improved performance.

Returns EmbeddingModel format which extends EmbeddingConfig with additional metadata fields.
Legacy EmbeddingConfig fields are marked as deprecated but still available for backward compatibility.

### Returns

- `display_name: string`

  Display name for the model shown in UI

- `embedding_dim: number`

  The dimension of the embedding

- `embedding_endpoint_type: "openai" or "anthropic" or "bedrock" or 16 more`

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

- `azure_deployment: optional string`

  Deprecated: The Azure deployment for the model.

- `azure_endpoint: optional string`

  Deprecated: The Azure endpoint for the model.

- `azure_version: optional string`

  Deprecated: The Azure version for the model.

- `batch_size: optional number`

  Deprecated: The maximum batch size for processing embeddings.

- `embedding_chunk_size: optional number`

  Deprecated: The chunk size of the embedding.

- `embedding_endpoint: optional string`

  Deprecated: The endpoint for the model.

- `handle: optional string`

  The handle for this config, in the format provider/model-name.

- `model_type: optional "embedding"`

  Type of model (llm or embedding)

  - `"embedding"`

### Example

```http
curl https://api.letta.com/v1/models/embedding \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

## Domain Types

### Embedding List Response

- `EmbeddingListResponse = array of EmbeddingModel`

  - `display_name: string`

    Display name for the model shown in UI

  - `embedding_dim: number`

    The dimension of the embedding

  - `embedding_endpoint_type: "openai" or "anthropic" or "bedrock" or 16 more`

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

  - `azure_deployment: optional string`

    Deprecated: The Azure deployment for the model.

  - `azure_endpoint: optional string`

    Deprecated: The Azure endpoint for the model.

  - `azure_version: optional string`

    Deprecated: The Azure version for the model.

  - `batch_size: optional number`

    Deprecated: The maximum batch size for processing embeddings.

  - `embedding_chunk_size: optional number`

    Deprecated: The chunk size of the embedding.

  - `embedding_endpoint: optional string`

    Deprecated: The endpoint for the model.

  - `handle: optional string`

    The handle for this config, in the format provider/model-name.

  - `model_type: optional "embedding"`

    Type of model (llm or embedding)

    - `"embedding"`
