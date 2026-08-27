## List Llm Models

`client.models.list(ModelListParamsquery?, RequestOptionsoptions?): ModelListResponse`

**get** `/v1/models/`

List available LLM models using the asynchronous implementation for improved performance.

Returns Model format which extends LLMConfig with additional metadata fields.
Legacy LLMConfig fields are marked as deprecated but still available for backward compatibility.

### Parameters

- `query: ModelListParams`

  - `provider_category?: Array<ProviderCategory> | null`

    - `"base"`

    - `"byok"`

  - `provider_name?: string | null`

  - `provider_type?: ProviderType | null`

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

- `ModelListResponse = Array<Model>`

  - `context_window: number`

    Deprecated: Use 'max_context_window' field instead. The context window size for the model.

  - `max_context_window: number`

    The maximum context window for the model

  - `model: string`

    Deprecated: Use 'name' field instead. LLM model name.

  - `model_endpoint_type: "openai" | "anthropic" | "google_ai" | 26 more`

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

  - `compatibility_type?: "gguf" | "mlx" | null`

    Deprecated: The framework compatibility type for the model.

    - `"gguf"`

    - `"mlx"`

  - `display_name?: string | null`

    A human-friendly display name for the model.

  - `effort?: "low" | "medium" | "high" | 2 more | null`

    The effort level for Anthropic models that support it (Opus 4.5+). Controls token spending and thinking behavior. Not setting this gives similar performance to 'high'.

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

    - `"max"`

  - `enable_reasoner?: boolean`

    Deprecated: Whether or not the model should use extended thinking if it is a 'reasoning' style model.

  - `frequency_penalty?: number | null`

    Deprecated: Positive values penalize new tokens based on their existing frequency in the text so far.

  - `handle?: string | null`

    The handle for this config, in the format provider/model-name.

  - `max_reasoning_tokens?: number`

    Deprecated: Configurable thinking budget for extended thinking.

  - `max_tokens?: number | null`

    Deprecated: The maximum number of tokens to generate.

  - `model_endpoint?: string | null`

    Deprecated: The endpoint for the model.

  - `model_type?: "llm"`

    Type of model (llm or embedding)

    - `"llm"`

  - `model_wrapper?: string | null`

    Deprecated: The wrapper for the model.

  - `parallel_tool_calls?: boolean | null`

    Deprecated: If set to True, enables parallel tool calling.

  - `provider_category?: ProviderCategory | null`

    Deprecated: The provider category for the model.

    - `"base"`

    - `"byok"`

  - `provider_name?: string | null`

    The provider name for the model.

  - `put_inner_thoughts_in_kwargs?: boolean | null`

    Deprecated: Puts 'inner_thoughts' as a kwarg in the function call.

  - `reasoning_effort?: "none" | "minimal" | "low" | 3 more | null`

    Deprecated: The reasoning effort to use when generating text reasoning models.

    - `"none"`

    - `"minimal"`

    - `"low"`

    - `"medium"`

    - `"high"`

    - `"xhigh"`

  - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

    The response format for the model's output. Supports text, json_object, and json_schema (structured outputs). Can be set via model_settings.

    - `TextResponseFormat`

      Response format for plain text responses.

      - `type?: "text"`

        The type of the response format.

        - `"text"`

    - `JsonSchemaResponseFormat`

      Response format for JSON schema-based responses.

      - `json_schema: Record<string, unknown>`

        The JSON schema of the response.

      - `type?: "json_schema"`

        The type of the response format.

        - `"json_schema"`

    - `JsonObjectResponseFormat`

      Response format for JSON object responses.

      - `type?: "json_object"`

        The type of the response format.

        - `"json_object"`

  - `return_logprobs?: boolean`

    Whether to return log probabilities of the output tokens. Useful for RL training.

  - `return_token_ids?: boolean`

    Whether to return token IDs for all LLM generations via SGLang native endpoint. Required for multi-turn RL training with loss masking. Only works with SGLang provider.

  - `strict?: boolean`

    Enable strict mode for tool calling. When true, tool schemas include strict: true and additionalProperties: false, guaranteeing tool outputs match JSON schemas.

  - `temperature?: number`

    Deprecated: The temperature to use when generating text with the model.

  - `tier?: string | null`

    Deprecated: The cost tier for the model (cloud only).

  - `tool_call_parser?: string | null`

    SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

  - `top_logprobs?: number | null`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `verbosity?: "low" | "medium" | "high" | null`

    Deprecated: Soft control for how verbose model output should be.

    - `"low"`

    - `"medium"`

    - `"high"`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const models = await client.models.list();

console.log(models);
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
