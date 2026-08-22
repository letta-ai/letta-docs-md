# Models

## List Llm Models

`models.list(ModelListParams**kwargs)  -> ModelListResponse`

**get** `/v1/models/`

List available LLM models using the asynchronous implementation for improved performance.

Returns Model format which extends LLMConfig with additional metadata fields.
Legacy LLMConfig fields are marked as deprecated but still available for backward compatibility.

### Parameters

- `provider_category: Optional[List[ProviderCategory]]`

  - `"base"`

  - `"byok"`

- `provider_name: Optional[str]`

- `provider_type: Optional[ProviderType]`

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

### Returns

- `List[Model]`

  - `context_window: int`

    Deprecated: Use 'max_context_window' field instead. The context window size for the model.

  - `max_context_window: int`

    The maximum context window for the model

  - `model: str`

    Deprecated: Use 'name' field instead. LLM model name.

  - `model_endpoint_type: Literal["openai", "anthropic", "google_ai", 26 more]`

    Deprecated: Use 'provider_type' field instead. The endpoint type for the model.

    - `"openai"`

    - `"anthropic"`

    - `"google_ai"`

    - `"google_vertex"`

    - `"azure"`

    - `"groq"`

    - `"ollama"`

    - `"webui"`

    - `"webui-legacy"`

    - `"lmstudio"`

    - `"lmstudio-legacy"`

    - `"lmstudio-chatcompletions"`

    - `"llamacpp"`

    - `"koboldcpp"`

    - `"vllm"`

    - `"hugging-face"`

    - `"baseten"`

    - `"minimax"`

    - `"moonshot"`

    - `"moonshot_coding"`

    - `"mistral"`

    - `"together"`

    - `"bedrock"`

    - `"deepseek"`

    - `"xai"`

    - `"zai"`

    - `"zai_coding"`

    - `"openrouter"`

    - `"chatgpt_oauth"`

  - `name: str`

    The actual model name used by the provider

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

  - `compatibility_type: Optional[Literal["gguf", "mlx"]]`

    Deprecated: The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name: Optional[str]`

    A human-friendly display name for the model.

  - `effort: Optional[Literal["low", "medium", "high", 2 more]]`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner: Optional[bool]`

    Deprecated: Whether or not the model should use extended thinking if it is a 'reasoning' style model.

  - `frequency_penalty: Optional[float]`

    Deprecated: Positive values penalize new tokens based on their existing frequency in the text so far.

  - `handle: Optional[str]`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens: Optional[int]`

    Deprecated: Configurable thinking budget for extended thinking.

  - `max_tokens: Optional[int]`

    Deprecated: The maximum number of tokens to generate.

  - `model_endpoint: Optional[str]`

    Deprecated: The endpoint for the model.

  - `model_type: Optional[Literal["llm"]]`

    Type of model (llm or embedding)

    - `"llm"`

  - `model_wrapper: Optional[str]`

    Deprecated: The wrapper for the model.

  - `parallel_tool_calls: Optional[bool]`

    Deprecated: If set to True, enables parallel tool calling.

  - `provider_category: Optional[ProviderCategory]`

    Deprecated: The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name: Optional[str]`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs: Optional[bool]`

    Deprecated: Puts 'inner_thoughts' as a kwarg in the function call.

  - `reasoning_effort: Optional[Literal["none", "minimal", "low", 3 more]]`

    Deprecated: The reasoning effort to use when generating text reasoning models.

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format: Optional[ResponseFormat]`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `class TextResponseFormat: …`

      Response format for plain text responses.

      - `type: Optional[Literal["text"]]`

        The type of the response format.

        - `"text"`

    - `class JsonSchemaResponseFormat: …`

      Response format for JSON schema-based responses.

      - `json_schema: Dict[str, object]`

        The JSON schema of the response.

      - `type: Optional[Literal["json_schema"]]`

        The type of the response format.

        - `"json_schema"`

    - `class JsonObjectResponseFormat: …`

      Response format for JSON object responses.

      - `type: Optional[Literal["json_object"]]`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs: Optional[bool]`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids: Optional[bool]`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict: Optional[bool]`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature: Optional[float]`

    Deprecated: The temperature to use when generating text with the model.

  - `tier: Optional[str]`

    Deprecated: The cost tier for the model (cloud only).

  - `tool_call_parser: Optional[str]`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs: Optional[int]`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity: Optional[Literal["low", "medium", "high"]]`

    Deprecated: Soft control for how verbose model output should be.

    - `"low"`

    - `"medium"`

    - `"high"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
models = client.models.list()
print(models)
```

#### Response

```json
[
  {
    "context_window": 0,
    "max_context_window": 0,
    "model": "model",
    "model_endpoint_type": "openai",
    "name": "name",
    "provider_type": "anthropic",
    "compatibility_type": "gguf",
    "display_name": "display_name",
    "effort": "low",
    "enable_reasoner": true,
    "frequency_penalty": 0,
    "handle": "handle",
    "max_reasoning_tokens": 0,
    "max_tokens": 0,
    "model_endpoint": "model_endpoint",
    "model_type": "llm",
    "model_wrapper": "model_wrapper",
    "parallel_tool_calls": true,
    "provider_category": "base",
    "provider_name": "provider_name",
    "put_inner_thoughts_in_kwargs": true,
    "reasoning_effort": "none",
    "response_format": {
      "type": "text"
    },
    "return_logprobs": true,
    "return_token_ids": true,
    "strict": true,
    "temperature": 0,
    "tier": "tier",
    "tool_call_parser": "tool_call_parser",
    "top_logprobs": 0,
    "verbosity": "low"
  }
]
```

## Domain Types

### Embedding Config

- `class EmbeddingConfig: …`

  Configuration for embedding model connection and processing parameters.

  - `embedding_dim: int`

    The dimension of the embedding.

  - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

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

  - `embedding_model: str`

    The model for the embedding.

  - `azure_deployment: Optional[str]`

    The Azure deployment for the model.

  - `azure_endpoint: Optional[str]`

    The Azure endpoint for the model.

  - `azure_version: Optional[str]`

    The Azure version for the model.

  - `batch_size: Optional[int]`

    The maximum batch size for processing embeddings.

  - `embedding_chunk_size: Optional[int]`

    The chunk size of the embedding.

  - `embedding_endpoint: Optional[str]`

    The endpoint for the model (`None` if local).

  - `handle: Optional[str]`

    The handle for this config, in the format provider/model-name.

### Embedding Model

- `class EmbeddingModel: …`

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

### Llm Config

- `class LlmConfig: …`

  Configuration for Language Model (LLM) connection and generation parameters.

  .. deprecated::
  LLMConfig is deprecated and should not be used as an input or return type in API calls.
  Use the schemas in letta.schemas.model (ModelSettings, OpenAIModelSettings, etc.) instead.
  For conversion, use the _to_model() method or Model._from_llm_config() method.

  - `context_window: int`

    The context window size for the model.

  - `model: str`

    LLM model name.

  - `model_endpoint_type: Literal["openai", "anthropic", "google_ai", 27 more]`

    The endpoint type for the model.

    - `"openai"`

    - `"anthropic"`

    - `"google_ai"`

    - `"google_vertex"`

    - `"azure"`

    - `"groq"`

    - `"ollama"`

    - `"webui"`

    - `"webui-legacy"`

    - `"lmstudio"`

    - `"lmstudio-legacy"`

    - `"lmstudio-chatcompletions"`

    - `"llamacpp"`

    - `"koboldcpp"`

    - `"vllm"`

    - `"hugging-face"`

    - `"minimax"`

    - `"moonshot"`

    - `"moonshot_coding"`

    - `"mistral"`

    - `"together"`

    - `"bedrock"`

    - `"deepseek"`

    - `"xai"`

    - `"zai"`

    - `"zai_coding"`

    - `"baseten"`

    - `"fireworks"`

    - `"openrouter"`

    - `"chatgpt_oauth"`

  - `compatibility_type: Optional[Literal["gguf", "mlx"]]`

    The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name: Optional[str]`

    A human-friendly display name for the model.

  - `effort: Optional[Literal["low", "medium", "high", 2 more]]`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner: Optional[bool]`

    Whether or not the model should use extended thinking if it is a 'reasoning' style model

  - `frequency_penalty: Optional[float]`

    Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim. From OpenAI: Number between -2.0 and 2.0.

  - `handle: Optional[str]`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens: Optional[int]`

    Configurable thinking budget for extended thinking. Used for enable_reasoner and also for Google Vertex models like Gemini 2.5 Flash. Minimum value is 1024 when used with enable_reasoner.

  - `max_tokens: Optional[int]`

    The maximum number of tokens to generate. If not set, the model will use its default value.

  - `model_endpoint: Optional[str]`

    The endpoint for the model.

  - `model_wrapper: Optional[str]`

    The wrapper for the model.

  - `parallel_tool_calls: Optional[bool]`

    Deprecated: Use model_settings to configure parallel tool calls instead. If set to True, enables parallel tool calling. Defaults to False.

  - `provider_category: Optional[ProviderCategory]`

    The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name: Optional[str]`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs: Optional[bool]`

    Puts 'inner_thoughts' as a kwarg in the function call if this is set to True. This helps with function calling performance and also the generation of inner thoughts.

  - `reasoning_effort: Optional[Literal["none", "minimal", "low", 3 more]]`

    The reasoning effort to use when generating text reasoning models

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format: Optional[ResponseFormat]`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `class TextResponseFormat: …`

      Response format for plain text responses.

      - `type: Optional[Literal["text"]]`

        The type of the response format.

        - `"text"`

    - `class JsonSchemaResponseFormat: …`

      Response format for JSON schema-based responses.

      - `json_schema: Dict[str, object]`

        The JSON schema of the response.

      - `type: Optional[Literal["json_schema"]]`

        The type of the response format.

        - `"json_schema"`

    - `class JsonObjectResponseFormat: …`

      Response format for JSON object responses.

      - `type: Optional[Literal["json_object"]]`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs: Optional[bool]`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids: Optional[bool]`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict: Optional[bool]`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature: Optional[float]`

    The temperature to use when generating text with the model. A higher temperature will result in more random text.

  - `tier: Optional[str]`

    The cost tier for the model (cloud only).

  - `tool_call_parser: Optional[str]`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs: Optional[int]`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity: Optional[Literal["low", "medium", "high"]]`

    Soft control for how verbose model output should be, used for GPT-5 models.

    - `"low"`

    - `"medium"`

    - `"high"`

### Model

- `class Model: …`

  - `context_window: int`

    Deprecated: Use 'max_context_window' field instead. The context window size for the model.

  - `max_context_window: int`

    The maximum context window for the model

  - `model: str`

    Deprecated: Use 'name' field instead. LLM model name.

  - `model_endpoint_type: Literal["openai", "anthropic", "google_ai", 26 more]`

    Deprecated: Use 'provider_type' field instead. The endpoint type for the model.

    - `"openai"`

    - `"anthropic"`

    - `"google_ai"`

    - `"google_vertex"`

    - `"azure"`

    - `"groq"`

    - `"ollama"`

    - `"webui"`

    - `"webui-legacy"`

    - `"lmstudio"`

    - `"lmstudio-legacy"`

    - `"lmstudio-chatcompletions"`

    - `"llamacpp"`

    - `"koboldcpp"`

    - `"vllm"`

    - `"hugging-face"`

    - `"baseten"`

    - `"minimax"`

    - `"moonshot"`

    - `"moonshot_coding"`

    - `"mistral"`

    - `"together"`

    - `"bedrock"`

    - `"deepseek"`

    - `"xai"`

    - `"zai"`

    - `"zai_coding"`

    - `"openrouter"`

    - `"chatgpt_oauth"`

  - `name: str`

    The actual model name used by the provider

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

  - `compatibility_type: Optional[Literal["gguf", "mlx"]]`

    Deprecated: The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name: Optional[str]`

    A human-friendly display name for the model.

  - `effort: Optional[Literal["low", "medium", "high", 2 more]]`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner: Optional[bool]`

    Deprecated: Whether or not the model should use extended thinking if it is a 'reasoning' style model.

  - `frequency_penalty: Optional[float]`

    Deprecated: Positive values penalize new tokens based on their existing frequency in the text so far.

  - `handle: Optional[str]`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens: Optional[int]`

    Deprecated: Configurable thinking budget for extended thinking.

  - `max_tokens: Optional[int]`

    Deprecated: The maximum number of tokens to generate.

  - `model_endpoint: Optional[str]`

    Deprecated: The endpoint for the model.

  - `model_type: Optional[Literal["llm"]]`

    Type of model (llm or embedding)

    - `"llm"`

  - `model_wrapper: Optional[str]`

    Deprecated: The wrapper for the model.

  - `parallel_tool_calls: Optional[bool]`

    Deprecated: If set to True, enables parallel tool calling.

  - `provider_category: Optional[ProviderCategory]`

    Deprecated: The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name: Optional[str]`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs: Optional[bool]`

    Deprecated: Puts 'inner_thoughts' as a kwarg in the function call.

  - `reasoning_effort: Optional[Literal["none", "minimal", "low", 3 more]]`

    Deprecated: The reasoning effort to use when generating text reasoning models.

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format: Optional[ResponseFormat]`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `class TextResponseFormat: …`

      Response format for plain text responses.

      - `type: Optional[Literal["text"]]`

        The type of the response format.

        - `"text"`

    - `class JsonSchemaResponseFormat: …`

      Response format for JSON schema-based responses.

      - `json_schema: Dict[str, object]`

        The JSON schema of the response.

      - `type: Optional[Literal["json_schema"]]`

        The type of the response format.

        - `"json_schema"`

    - `class JsonObjectResponseFormat: …`

      Response format for JSON object responses.

      - `type: Optional[Literal["json_object"]]`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs: Optional[bool]`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids: Optional[bool]`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict: Optional[bool]`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature: Optional[float]`

    Deprecated: The temperature to use when generating text with the model.

  - `tier: Optional[str]`

    Deprecated: The cost tier for the model (cloud only).

  - `tool_call_parser: Optional[str]`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs: Optional[int]`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity: Optional[Literal["low", "medium", "high"]]`

    Deprecated: Soft control for how verbose model output should be.

    - `"low"`

    - `"medium"`

    - `"high"`

### Provider Category

- `Literal["base", "byok"]`

  - `"base"`

  - `"byok"`

### Provider Type

- `Literal["anthropic", "azure", "baseten", 24 more]`

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

### Model List Response

- `List[Model]`

  - `context_window: int`

    Deprecated: Use 'max_context_window' field instead. The context window size for the model.

  - `max_context_window: int`

    The maximum context window for the model

  - `model: str`

    Deprecated: Use 'name' field instead. LLM model name.

  - `model_endpoint_type: Literal["openai", "anthropic", "google_ai", 26 more]`

    Deprecated: Use 'provider_type' field instead. The endpoint type for the model.

    - `"openai"`

    - `"anthropic"`

    - `"google_ai"`

    - `"google_vertex"`

    - `"azure"`

    - `"groq"`

    - `"ollama"`

    - `"webui"`

    - `"webui-legacy"`

    - `"lmstudio"`

    - `"lmstudio-legacy"`

    - `"lmstudio-chatcompletions"`

    - `"llamacpp"`

    - `"koboldcpp"`

    - `"vllm"`

    - `"hugging-face"`

    - `"baseten"`

    - `"minimax"`

    - `"moonshot"`

    - `"moonshot_coding"`

    - `"mistral"`

    - `"together"`

    - `"bedrock"`

    - `"deepseek"`

    - `"xai"`

    - `"zai"`

    - `"zai_coding"`

    - `"openrouter"`

    - `"chatgpt_oauth"`

  - `name: str`

    The actual model name used by the provider

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

  - `compatibility_type: Optional[Literal["gguf", "mlx"]]`

    Deprecated: The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name: Optional[str]`

    A human-friendly display name for the model.

  - `effort: Optional[Literal["low", "medium", "high", 2 more]]`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner: Optional[bool]`

    Deprecated: Whether or not the model should use extended thinking if it is a 'reasoning' style model.

  - `frequency_penalty: Optional[float]`

    Deprecated: Positive values penalize new tokens based on their existing frequency in the text so far.

  - `handle: Optional[str]`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens: Optional[int]`

    Deprecated: Configurable thinking budget for extended thinking.

  - `max_tokens: Optional[int]`

    Deprecated: The maximum number of tokens to generate.

  - `model_endpoint: Optional[str]`

    Deprecated: The endpoint for the model.

  - `model_type: Optional[Literal["llm"]]`

    Type of model (llm or embedding)

    - `"llm"`

  - `model_wrapper: Optional[str]`

    Deprecated: The wrapper for the model.

  - `parallel_tool_calls: Optional[bool]`

    Deprecated: If set to True, enables parallel tool calling.

  - `provider_category: Optional[ProviderCategory]`

    Deprecated: The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name: Optional[str]`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs: Optional[bool]`

    Deprecated: Puts 'inner_thoughts' as a kwarg in the function call.

  - `reasoning_effort: Optional[Literal["none", "minimal", "low", 3 more]]`

    Deprecated: The reasoning effort to use when generating text reasoning models.

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format: Optional[ResponseFormat]`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `class TextResponseFormat: …`

      Response format for plain text responses.

      - `type: Optional[Literal["text"]]`

        The type of the response format.

        - `"text"`

    - `class JsonSchemaResponseFormat: …`

      Response format for JSON schema-based responses.

      - `json_schema: Dict[str, object]`

        The JSON schema of the response.

      - `type: Optional[Literal["json_schema"]]`

        The type of the response format.

        - `"json_schema"`

    - `class JsonObjectResponseFormat: …`

      Response format for JSON object responses.

      - `type: Optional[Literal["json_object"]]`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs: Optional[bool]`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids: Optional[bool]`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict: Optional[bool]`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature: Optional[float]`

    Deprecated: The temperature to use when generating text with the model.

  - `tier: Optional[str]`

    Deprecated: The cost tier for the model (cloud only).

  - `tool_call_parser: Optional[str]`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs: Optional[int]`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity: Optional[Literal["low", "medium", "high"]]`

    Deprecated: Soft control for how verbose model output should be.

    - `"low"`

    - `"medium"`

    - `"high"`

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
