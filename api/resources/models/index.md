# Models

## List Llm Models

**get** `/v1/models/`

List available LLM models using the asynchronous implementation for improved performance.

Returns Model format which extends LLMConfig with additional metadata fields.
Legacy LLMConfig fields are marked as deprecated but still available for backward compatibility.

### Query Parameters

- `provider_category: optional array of ProviderCategory`

  - `"base"`

  - `"byok"`

- `provider_name: optional string`

- `provider_type: optional ProviderType`

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

- `context_window: number`

  Deprecated: Use 'max_context_window' field instead. The context window size for the model.

- `max_context_window: number`

  The maximum context window for the model

- `model: string`

  Deprecated: Use 'name' field instead. LLM model name.

- `model_endpoint_type: "openai" or "anthropic" or "google_ai" or 26 more`

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

- `name: string`

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

- `compatibility_type: optional "gguf" or "mlx"`

  Deprecated: The framework compatibility type for the model.

  - `"gguf"`

  - `"mlx"`

- `display_name: optional string`

  A human-friendly display name for the model.

- `effort: optional "low" or "medium" or "high" or 2 more`

  The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

  - `"low"`

  - `"medium"`

  - `"high"`

  - `"xhigh"`

  - `"max"`

- `enable_reasoner: optional boolean`

  Deprecated: Whether or not the model should use extended thinking if it is a 'reasoning' style model.

- `frequency_penalty: optional number`

  Deprecated: Positive values penalize new tokens based on their existing frequency in the text so far.

- `handle: optional string`

  The handle for this config, in the format provider/model-name.

- `max_reasoning_tokens: optional number`

  Deprecated: Configurable thinking budget for extended thinking.

- `max_tokens: optional number`

  Deprecated: The maximum number of tokens to generate.

- `model_endpoint: optional string`

  Deprecated: The endpoint for the model.

- `model_type: optional "llm"`

  Type of model (llm or embedding)

  - `"llm"`

- `model_wrapper: optional string`

  Deprecated: The wrapper for the model.

- `parallel_tool_calls: optional boolean`

  Deprecated: If set to True, enables parallel tool calling.

- `provider_category: optional ProviderCategory`

  Deprecated: The provider category for the model.

  - `"base"`

  - `"byok"`

- `provider_name: optional string`

  The provider name for the model.

- `put_inner_thoughts_in_kwargs: optional boolean`

  Deprecated: Puts 'inner_thoughts' as a kwarg in the function call.

- `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

  Deprecated: The reasoning effort to use when generating text reasoning models.

  - `"none"`

  - `"minimal"`

  - `"low"`

  - `"medium"`

  - `"high"`

  - `"xhigh"`

- `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

  The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

  - `TextResponseFormat object { type }`

    Response format for plain text responses.

    - `type: optional "text"`

      The type of the response format.

      - `"text"`

  - `JsonSchemaResponseFormat object { json_schema, type }`

    Response format for JSON schema-based responses.

    - `json_schema: map[unknown]`

      The JSON schema of the response.

    - `type: optional "json_schema"`

      The type of the response format.

      - `"json_schema"`

  - `JsonObjectResponseFormat object { type }`

    Response format for JSON object responses.

    - `type: optional "json_object"`

      The type of the response format.

      - `"json_object"`

- `return_logprobs: optional boolean`

  Whether to return log probabilities of the output tokens. Useful for RL training.

- `return_token_ids: optional boolean`

  Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

- `strict: optional boolean`

  Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

- `temperature: optional number`

  Deprecated: The temperature to use when generating text with the model.

- `tier: optional string`

  Deprecated: The cost tier for the model (cloud only).

- `tool_call_parser: optional string`

  SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

- `top_logprobs: optional number`

  Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

- `verbosity: optional "low" or "medium" or "high"`

  Deprecated: Soft control for how verbose model output should be.

  - `"low"`

  - `"medium"`

  - `"high"`

### Example

```http
curl https://api.letta.com/v1/models/ \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

- `EmbeddingConfig object { embedding_dim, embedding_endpoint_type, embedding_model, 7 more }`

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

### Embedding Model

- `EmbeddingModel object { display_name, embedding_dim, embedding_endpoint_type, 12 more }`

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

### Llm Config

- `LlmConfig object { context_window, model, model_endpoint_type, 24 more }`

  Configuration for Language Model (LLM) connection and generation parameters.

  .. deprecated::
  LLMConfig is deprecated and should not be used as an input or return type in API calls.
  Use the schemas in letta.schemas.model (ModelSettings, OpenAIModelSettings, etc.) instead.
  For conversion, use the _to_model() method or Model._from_llm_config() method.

  - `context_window: number`

    The context window size for the model.

  - `model: string`

    LLM model name.

  - `model_endpoint_type: "openai" or "anthropic" or "google_ai" or 27 more`

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

  - `compatibility_type: optional "gguf" or "mlx"`

    The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name: optional string`

    A human-friendly display name for the model.

  - `effort: optional "low" or "medium" or "high" or 2 more`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner: optional boolean`

    Whether or not the model should use extended thinking if it is a 'reasoning' style model

  - `frequency_penalty: optional number`

    Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim. From OpenAI: Number between -2.0 and 2.0.

  - `handle: optional string`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens: optional number`

    Configurable thinking budget for extended thinking. Used for enable_reasoner and also for Google Vertex models like Gemini 2.5 Flash. Minimum value is 1024 when used with enable_reasoner.

  - `max_tokens: optional number`

    The maximum number of tokens to generate. If not set, the model will use its default value.

  - `model_endpoint: optional string`

    The endpoint for the model.

  - `model_wrapper: optional string`

    The wrapper for the model.

  - `parallel_tool_calls: optional boolean`

    Deprecated: Use model_settings to configure parallel tool calls instead. If set to True, enables parallel tool calling. Defaults to False.

  - `provider_category: optional ProviderCategory`

    The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name: optional string`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs: optional boolean`

    Puts 'inner_thoughts' as a kwarg in the function call if this is set to True. This helps with function calling performance and also the generation of inner thoughts.

  - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

    The reasoning effort to use when generating text reasoning models

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `TextResponseFormat object { type }`

      Response format for plain text responses.

      - `type: optional "text"`

        The type of the response format.

        - `"text"`

    - `JsonSchemaResponseFormat object { json_schema, type }`

      Response format for JSON schema-based responses.

      - `json_schema: map[unknown]`

        The JSON schema of the response.

      - `type: optional "json_schema"`

        The type of the response format.

        - `"json_schema"`

    - `JsonObjectResponseFormat object { type }`

      Response format for JSON object responses.

      - `type: optional "json_object"`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs: optional boolean`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids: optional boolean`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict: optional boolean`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature: optional number`

    The temperature to use when generating text with the model. A higher temperature will result in more random text.

  - `tier: optional string`

    The cost tier for the model (cloud only).

  - `tool_call_parser: optional string`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs: optional number`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity: optional "low" or "medium" or "high"`

    Soft control for how verbose model output should be, used for GPT-5 models.

    - `"low"`

    - `"medium"`

    - `"high"`

### Model

- `Model object { context_window, max_context_window, model, 28 more }`

  - `context_window: number`

    Deprecated: Use 'max_context_window' field instead. The context window size for the model.

  - `max_context_window: number`

    The maximum context window for the model

  - `model: string`

    Deprecated: Use 'name' field instead. LLM model name.

  - `model_endpoint_type: "openai" or "anthropic" or "google_ai" or 26 more`

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

  - `name: string`

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

  - `compatibility_type: optional "gguf" or "mlx"`

    Deprecated: The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name: optional string`

    A human-friendly display name for the model.

  - `effort: optional "low" or "medium" or "high" or 2 more`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner: optional boolean`

    Deprecated: Whether or not the model should use extended thinking if it is a 'reasoning' style model.

  - `frequency_penalty: optional number`

    Deprecated: Positive values penalize new tokens based on their existing frequency in the text so far.

  - `handle: optional string`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens: optional number`

    Deprecated: Configurable thinking budget for extended thinking.

  - `max_tokens: optional number`

    Deprecated: The maximum number of tokens to generate.

  - `model_endpoint: optional string`

    Deprecated: The endpoint for the model.

  - `model_type: optional "llm"`

    Type of model (llm or embedding)

    - `"llm"`

  - `model_wrapper: optional string`

    Deprecated: The wrapper for the model.

  - `parallel_tool_calls: optional boolean`

    Deprecated: If set to True, enables parallel tool calling.

  - `provider_category: optional ProviderCategory`

    Deprecated: The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name: optional string`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs: optional boolean`

    Deprecated: Puts 'inner_thoughts' as a kwarg in the function call.

  - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

    Deprecated: The reasoning effort to use when generating text reasoning models.

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `TextResponseFormat object { type }`

      Response format for plain text responses.

      - `type: optional "text"`

        The type of the response format.

        - `"text"`

    - `JsonSchemaResponseFormat object { json_schema, type }`

      Response format for JSON schema-based responses.

      - `json_schema: map[unknown]`

        The JSON schema of the response.

      - `type: optional "json_schema"`

        The type of the response format.

        - `"json_schema"`

    - `JsonObjectResponseFormat object { type }`

      Response format for JSON object responses.

      - `type: optional "json_object"`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs: optional boolean`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids: optional boolean`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict: optional boolean`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature: optional number`

    Deprecated: The temperature to use when generating text with the model.

  - `tier: optional string`

    Deprecated: The cost tier for the model (cloud only).

  - `tool_call_parser: optional string`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs: optional number`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity: optional "low" or "medium" or "high"`

    Deprecated: Soft control for how verbose model output should be.

    - `"low"`

    - `"medium"`

    - `"high"`

### Provider Category

- `ProviderCategory = "base" or "byok"`

  - `"base"`

  - `"byok"`

### Provider Type

- `ProviderType = "anthropic" or "azure" or "baseten" or 24 more`

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

- `ModelListResponse = array of Model`

  - `context_window: number`

    Deprecated: Use 'max_context_window' field instead. The context window size for the model.

  - `max_context_window: number`

    The maximum context window for the model

  - `model: string`

    Deprecated: Use 'name' field instead. LLM model name.

  - `model_endpoint_type: "openai" or "anthropic" or "google_ai" or 26 more`

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

  - `name: string`

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

  - `compatibility_type: optional "gguf" or "mlx"`

    Deprecated: The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name: optional string`

    A human-friendly display name for the model.

  - `effort: optional "low" or "medium" or "high" or 2 more`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner: optional boolean`

    Deprecated: Whether or not the model should use extended thinking if it is a 'reasoning' style model.

  - `frequency_penalty: optional number`

    Deprecated: Positive values penalize new tokens based on their existing frequency in the text so far.

  - `handle: optional string`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens: optional number`

    Deprecated: Configurable thinking budget for extended thinking.

  - `max_tokens: optional number`

    Deprecated: The maximum number of tokens to generate.

  - `model_endpoint: optional string`

    Deprecated: The endpoint for the model.

  - `model_type: optional "llm"`

    Type of model (llm or embedding)

    - `"llm"`

  - `model_wrapper: optional string`

    Deprecated: The wrapper for the model.

  - `parallel_tool_calls: optional boolean`

    Deprecated: If set to True, enables parallel tool calling.

  - `provider_category: optional ProviderCategory`

    Deprecated: The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name: optional string`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs: optional boolean`

    Deprecated: Puts 'inner_thoughts' as a kwarg in the function call.

  - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

    Deprecated: The reasoning effort to use when generating text reasoning models.

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `TextResponseFormat object { type }`

      Response format for plain text responses.

      - `type: optional "text"`

        The type of the response format.

        - `"text"`

    - `JsonSchemaResponseFormat object { json_schema, type }`

      Response format for JSON schema-based responses.

      - `json_schema: map[unknown]`

        The JSON schema of the response.

      - `type: optional "json_schema"`

        The type of the response format.

        - `"json_schema"`

    - `JsonObjectResponseFormat object { type }`

      Response format for JSON object responses.

      - `type: optional "json_object"`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs: optional boolean`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids: optional boolean`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict: optional boolean`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature: optional number`

    Deprecated: The temperature to use when generating text with the model.

  - `tier: optional string`

    Deprecated: The cost tier for the model (cloud only).

  - `tool_call_parser: optional string`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs: optional number`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity: optional "low" or "medium" or "high"`

    Deprecated: Soft control for how verbose model output should be.

    - `"low"`

    - `"medium"`

    - `"high"`

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
