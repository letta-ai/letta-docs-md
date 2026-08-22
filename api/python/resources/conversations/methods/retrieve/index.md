## Retrieve Conversation

`conversations.retrieve(strconversation_id)  -> Conversation`

**get** `/v1/conversations/{conversation_id}`

Retrieve a specific conversation.

### Parameters

- `conversation_id: str`

  The ID of the conv in the format 'conv-<uuid4>'

### Returns

- `class Conversation: …`

  Represents a conversation on an agent for concurrent messaging.

  - `id: str`

    The unique identifier of the conversation.

  - `agent_id: str`

    The ID of the agent this conversation belongs to.

  - `archived: Optional[bool]`

    Whether the conversation is archived.

  - `archived_at: Optional[datetime]`

    Timestamp of when the conversation was archived.

  - `context_window_limit: Optional[int]`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at: Optional[datetime]`

    The timestamp when the object was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `description: Optional[str]`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids: Optional[List[str]]`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at: Optional[datetime]`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `model: Optional[str]`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: Optional[ModelSettings]`

    The model settings for this conversation (overrides agent's model settings).

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

    - `class ModelSettingsSgLangModelSettings: …`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["sglang"]]`

        The type of the provider.

        - `"sglang"`

      - `reasoning: Optional[ModelSettingsSgLangModelSettingsReasoning]`

        The reasoning configuration for the model.

        - `reasoning_effort: Optional[Literal["none", "minimal", "low", 3 more]]`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: Optional[ModelSettingsSgLangModelSettingsResponseFormat]`

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

    - `class ModelSettingsMoonshotModelSettings: …`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["moonshot"]]`

        The type of the provider.

        - `"moonshot"`

      - `response_format: Optional[ModelSettingsMoonshotModelSettingsResponseFormat]`

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

    - `class ModelSettingsZaiModelSettings: …`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["zai"]]`

        The type of the provider.

        - `"zai"`

      - `response_format: Optional[ModelSettingsZaiModelSettingsResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

      - `thinking: Optional[ModelSettingsZaiModelSettingsThinking]`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: Optional[bool]`

          If False, preserved thinking is used (recommended for agents).

        - `type: Optional[Literal["enabled", "disabled"]]`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `class ModelSettingsMoonshotCodingModelSettings: …`

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

      - `response_format: Optional[ModelSettingsMoonshotCodingModelSettingsResponseFormat]`

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

      - `thinking: Optional[ModelSettingsMoonshotCodingModelSettingsThinking]`

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

    - `class ModelSettingsBasetenModelSettings: …`

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

    - `class ModelSettingsOpenRouterModelSettings: …`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["openrouter"]]`

        The type of the provider.

        - `"openrouter"`

      - `response_format: Optional[ModelSettingsOpenRouterModelSettingsResponseFormat]`

        The response format for the model.

        - `class TextResponseFormat: …`

          Response format for plain text responses.

        - `class JsonSchemaResponseFormat: …`

          Response format for JSON schema-based responses.

        - `class JsonObjectResponseFormat: …`

          Response format for JSON object responses.

      - `temperature: Optional[float]`

        The temperature of the model.

    - `class ModelSettingsChatGptoAuthModelSettings: …`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: Optional[int]`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: Optional[bool]`

        Whether to enable parallel tool calling.

      - `provider_type: Optional[Literal["chatgpt_oauth"]]`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: Optional[ModelSettingsChatGptoAuthModelSettingsReasoning]`

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

  - `summary: Optional[str]`

    A summary of the conversation.

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
conversation = client.conversations.retrieve(
    "conv-123e4567-e89b-42d3-8456-426614174000",
)
print(conversation.id)
```

#### Response

```json
{
  "id": "id",
  "agent_id": "agent_id",
  "archived": true,
  "archived_at": "2019-12-27T18:11:19.117Z",
  "context_window_limit": 0,
  "created_at": "2019-12-27T18:11:19.117Z",
  "created_by_id": "created_by_id",
  "description": "description",
  "in_context_message_ids": [
    "string"
  ],
  "last_message_at": "2019-12-27T18:11:19.117Z",
  "last_updated_by_id": "last_updated_by_id",
  "model": "model",
  "model_settings": {
    "max_output_tokens": 0,
    "parallel_tool_calls": true,
    "provider_type": "openai",
    "reasoning": {
      "reasoning_effort": "none"
    },
    "response_format": {
      "type": "text"
    },
    "strict": true,
    "temperature": 0
  },
  "summary": "summary",
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```
