## Compact Conversation

`conversations.messages.compact(strconversation_id, MessageCompactParams**kwargs)  -> CompactionResponse`

**post** `/v1/conversations/{conversation_id}/compact`

Compact (summarize) a conversation's message history.

This endpoint summarizes the in-context messages for a specific conversation,
reducing the message count while preserving important context.

**Agent-direct mode**: Pass conversation_id="default" with agent_id in request body
to compact the agent's default conversation messages.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Parameters

- `conversation_id: str`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

- `agent_id: Optional[str]`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `compaction_settings: Optional[CompactionSettings]`

  Configuration for conversation compaction / summarization.

  Per-model settings (temperature,
  max tokens, etc.) are derived from the default configuration for that handle.

  - `clip_chars: Optional[int]`

    The maximum length of the summary in characters. If none, no clipping is performed.

  - `mode: Optional[Literal["all", "sliding_window", "self_compact_all", "self_compact_sliding_window"]]`

    The type of summarization technique use.

    - `"all"`

    - `"sliding_window"`

    - `"self_compact_all"`

    - `"self_compact_sliding_window"`

  - `model: Optional[str]`

    Model handle to use for sliding_window/all summarization (format: provider/model-name). If None, uses lightweight provider-specific defaults.

  - `model_settings: Optional[CompactionSettingsModelSettings]`

    Optional model settings used to override defaults for the summarizer model.

    - `class OpenAIModelSettings: …`

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["openai"]]`

        The type of the provider.

        - `"openai"`

      - `reasoning: Optional[Reasoning]`

        The reasoning configuration for the model.

        - `reasoning_effort: Optional[Literal["none", "minimal", "low", 3 more]]`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

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

      - `strict: Optional[bool]`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class CompactionSettingsModelSettingsSgLangModelSettings: …`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["sglang"]]`

        The type of the provider.

        - `"sglang"`

      - `reasoning: Optional[CompactionSettingsModelSettingsSgLangModelSettingsReasoning]`

        The reasoning configuration for the model.

        - `reasoning_effort: Optional[Literal["none", "minimal", "low", 3 more]]`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: Optional[CompactionSettingsModelSettingsSgLangModelSettingsResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `strict: Optional[bool]`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: Optional[float]`

        The temperature of the model.

      - `tool_call_parser: Optional[str]`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `class AnthropicModelSettings: …`

      - `effort: Optional[Literal["low", "medium", "high", 2 more]]`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["anthropic"]]`

        The type of the provider.

        - `"anthropic"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `strict: Optional[bool]`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: Optional[float]`

        The temperature of the model.

      - `thinking: Optional[Thinking]`

        The thinking configuration for the model.

        - `budget_tokens: Optional[int]`

          The maximum number of tokens the model can use for extended thinking.

        - `type: Optional[Literal["enabled", "disabled"]]`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: Optional[Literal["low", "medium", "high"]]`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `class GoogleAIModelSettings: …`

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["google_ai"]]`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: Optional[ResponseSchema]`

        The response schema for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

      - `thinking_config: Optional[ThinkingConfig]`

        The thinking configuration for the model.

        - `include_thoughts: Optional[bool]`

          Whether to include thoughts in the model's response.

        - `thinking_budget: Optional[int]`

          The thinking budget for the model.

    - `class GoogleVertexModelSettings: …`

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["google_vertex"]]`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: Optional[ResponseSchema]`

        The response schema for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

      - `thinking_config: Optional[ThinkingConfig]`

        The thinking configuration for the model.

        - `include_thoughts: Optional[bool]`

          Whether to include thoughts in the model's response.

        - `thinking_budget: Optional[int]`

          The thinking budget for the model.

    - `class AzureModelSettings: …`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["azure"]]`

        The type of the provider.

        - `"azure"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class XaiModelSettings: …`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["xai"]]`

        The type of the provider.

        - `"xai"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class CompactionSettingsModelSettingsMoonshotModelSettings: …`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["moonshot"]]`

        The type of the provider.

        - `"moonshot"`

      - `response_format: Optional[CompactionSettingsModelSettingsMoonshotModelSettingsResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `strict: Optional[bool]`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class CompactionSettingsModelSettingsZaiModelSettings: …`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["zai"]]`

        The type of the provider.

        - `"zai"`

      - `response_format: Optional[CompactionSettingsModelSettingsZaiModelSettingsResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

      - `thinking: Optional[CompactionSettingsModelSettingsZaiModelSettingsThinking]`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: Optional[bool]`

          If False, preserved thinking is used (recommended for agents).

        - `type: Optional[Literal["enabled", "disabled"]]`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `class CompactionSettingsModelSettingsMoonshotCodingModelSettings: …`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: Optional[Literal["low", "medium", "high", 2 more]]`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["moonshot_coding"]]`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: Optional[CompactionSettingsModelSettingsMoonshotCodingModelSettingsResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `strict: Optional[bool]`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: Optional[float]`

        The temperature of the model.

      - `thinking: Optional[CompactionSettingsModelSettingsMoonshotCodingModelSettingsThinking]`

        The thinking configuration for the model.

        - `budget_tokens: Optional[int]`

          The maximum number of tokens the model can use for extended thinking.

        - `type: Optional[Literal["enabled", "disabled"]]`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: Optional[Literal["low", "medium", "high"]]`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `class GroqModelSettings: …`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["groq"]]`

        The type of the provider.

        - `"groq"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class DeepseekModelSettings: …`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["deepseek"]]`

        The type of the provider.

        - `"deepseek"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class TogetherModelSettings: …`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["together"]]`

        The type of the provider.

        - `"together"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class BedrockModelSettings: …`

      AWS Bedrock model configuration.

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["bedrock"]]`

        The type of the provider.

        - `"bedrock"`

      - `response_format: Optional[ResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class CompactionSettingsModelSettingsBasetenModelSettings: …`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["baseten"]]`

        The type of the provider.

        - `"baseten"`

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class CompactionSettingsModelSettingsOpenRouterModelSettings: …`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["openrouter"]]`

        The type of the provider.

        - `"openrouter"`

      - `response_format: Optional[CompactionSettingsModelSettingsOpenRouterModelSettingsResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class CompactionSettingsModelSettingsChatGptoAuthModelSettings: …`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["chatgpt_oauth"]]`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: Optional[CompactionSettingsModelSettingsChatGptoAuthModelSettingsReasoning]`

        The reasoning configuration for the model.

        - `reasoning_effort: Optional[Literal["none", "low", "medium", 2 more]]`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: Optional[float]`

        The temperature of the model.

  - `prompt: Optional[str]`

    The prompt to use for summarization. If None, uses mode-specific default.

  - `prompt_acknowledgement: Optional[bool]`

    Whether to include an acknowledgement post-prompt (helps prevent non-summary outputs).

  - `sliding_window_percentage: Optional[float]`

    The percentage of the context window to keep post-summarization (only used in sliding window modes).

### Returns

- `class CompactionResponse: …`

  - `num_messages_after: int`

  - `num_messages_before: int`

  - `summary: str`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
compaction_response = client.conversations.messages.compact(
    conversation_id="default",
)
print(compaction_response.num_messages_after)
```

#### Response

```json
{
  "num_messages_after": 0,
  "num_messages_before": 0,
  "summary": "summary"
}
```
