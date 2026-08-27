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
