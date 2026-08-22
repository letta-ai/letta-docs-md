# Embeddings

## List Embedding Models

`models.embeddings.list()  -> EmbeddingListResponse`

**get** `/v1/models/embedding`

List available embedding models using the asynchronous implementation for improved performance.

Returns EmbeddingModel format which extends EmbeddingConfig with additional metadata fields.
Legacy EmbeddingConfig fields are marked as deprecated but still available for backward compatibility.

### Returns

- `List[EmbeddingModel]`

  - `display_name: str`

    Display name for the model shown in UI

  - `embedding_dim: int`

    The dimension of the embedding

  - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

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

  - `embedding_model: str`

    Deprecated: Use 'name' field instead. Embedding model name.

  - `name: str`

    The actual model name used by the provider

  - `provider_name: str`

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

  - `azure_deployment: Optional[str]`

    Deprecated: The Azure deployment for the model.

  - `azure_endpoint: Optional[str]`

    Deprecated: The Azure endpoint for the model.

  - `azure_version: Optional[str]`

    Deprecated: The Azure version for the model.

  - `batch_size: Optional[int]`

    Deprecated: The maximum batch size for processing embeddings.

  - `embedding_chunk_size: Optional[int]`

    Deprecated: The chunk size of the embedding.

  - `embedding_endpoint: Optional[str]`

    Deprecated: The endpoint for the model.

  - `handle: Optional[str]`

    The handle for this config, in the format provider/model-name.

  - `model_type: Optional[Literal["embedding"]]`

    Type of model (llm or embedding)

    - `"embedding"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
embedding_models = client.models.embeddings.list()
print(embedding_models)
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

- `List[EmbeddingModel]`

  - `display_name: str`

    Display name for the model shown in UI

  - `embedding_dim: int`

    The dimension of the embedding

  - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

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

  - `embedding_model: str`

    Deprecated: Use 'name' field instead. Embedding model name.

  - `name: str`

    The actual model name used by the provider

  - `provider_name: str`

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

  - `azure_deployment: Optional[str]`

    Deprecated: The Azure deployment for the model.

  - `azure_endpoint: Optional[str]`

    Deprecated: The Azure endpoint for the model.

  - `azure_version: Optional[str]`

    Deprecated: The Azure version for the model.

  - `batch_size: Optional[int]`

    Deprecated: The maximum batch size for processing embeddings.

  - `embedding_chunk_size: Optional[int]`

    Deprecated: The chunk size of the embedding.

  - `embedding_endpoint: Optional[str]`

    Deprecated: The endpoint for the model.

  - `handle: Optional[str]`

    The handle for this config, in the format provider/model-name.

  - `model_type: Optional[Literal["embedding"]]`

    Type of model (llm or embedding)

    - `"embedding"`
