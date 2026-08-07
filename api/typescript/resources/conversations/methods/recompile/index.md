## Recompile Conversation

`client.conversations.recompile(stringconversationID, ConversationRecompileParamsparams?, RequestOptionsoptions?): ConversationRecompileResponse`

**post** `/v1/conversations/{conversation_id}/recompile`

Manually trigger system prompt recompilation for a conversation.

### Parameters

- `conversationID: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

- `params: ConversationRecompileParams`

  - `dry_run?: boolean`

    Query param: If True, do not persist changes; still returns the compiled system prompt.

  - `agent_id?: string | null`

    Body param: Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

  - `compaction_settings?: CompactionSettings | null`

    Body param: Configuration for conversation compaction / summarization.

    Per-model settings (temperature,
    max tokens, etc.) are derived from the default configuration for that handle.

    - `clip_chars?: number | null`

      The maximum length of the summary in characters. If none, no clipping is performed.

    - `mode?: "all" | "sliding_window" | "self_compact_all" | "self_compact_sliding_window"`

      The type of summarization technique use.

      - `"all"`

      - `"sliding_window"`

      - `"self_compact_all"`

      - `"self_compact_sliding_window"`

    - `model?: string | null`

      Model handle to use for sliding_window/all summarization (format: provider/model-name). If None, uses lightweight provider-specific defaults.

    - `model_settings?: OpenAIModelSettings | SgLangModelSettings | AnthropicModelSettings | 14 more | null`

      Optional model settings used to override defaults for the summarizer model.

      - `OpenAIModelSettings`

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "openai"`

          The type of the provider.

          - `"openai"`

        - `reasoning?: Reasoning`

          The reasoning configuration for the model.

          - `reasoning_effort?: "none" | "minimal" | "low" | 3 more`

            The reasoning effort to use when generating text reasoning models

            - `"none"`

            - `"minimal"`

            - `"low"`

            - `"medium"`

            - `"high"`

            - `"xhigh"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

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

        - `strict?: boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature?: number`

          The temperature of the model.

      - `SgLangModelSettings`

        SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "sglang"`

          The type of the provider.

          - `"sglang"`

        - `reasoning?: Reasoning`

          The reasoning configuration for the model.

          - `reasoning_effort?: "none" | "minimal" | "low" | 3 more`

            The reasoning effort to use when generating text reasoning models

            - `"none"`

            - `"minimal"`

            - `"low"`

            - `"medium"`

            - `"high"`

            - `"xhigh"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `strict?: boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature?: number`

          The temperature of the model.

        - `tool_call_parser?: string | null`

          SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

      - `AnthropicModelSettings`

        - `effort?: "low" | "medium" | "high" | 2 more | null`

          Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

          - `"max"`

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "anthropic"`

          The type of the provider.

          - `"anthropic"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `strict?: boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature?: number`

          The temperature of the model.

        - `thinking?: Thinking`

          The thinking configuration for the model.

          - `budget_tokens?: number`

            The maximum number of tokens the model can use for extended thinking.

          - `type?: "enabled" | "disabled"`

            The type of thinking to use.

            - `"enabled"`

            - `"disabled"`

        - `verbosity?: "low" | "medium" | "high" | null`

          Soft control for how verbose model output should be, used for GPT-5 models.

          - `"low"`

          - `"medium"`

          - `"high"`

      - `GoogleAIModelSettings`

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "google_ai"`

          The type of the provider.

          - `"google_ai"`

        - `response_schema?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response schema for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

        - `thinking_config?: ThinkingConfig`

          The thinking configuration for the model.

          - `include_thoughts?: boolean`

            Whether to include thoughts in the model's response.

          - `thinking_budget?: number`

            The thinking budget for the model.

      - `GoogleVertexModelSettings`

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "google_vertex"`

          The type of the provider.

          - `"google_vertex"`

        - `response_schema?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response schema for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

        - `thinking_config?: ThinkingConfig`

          The thinking configuration for the model.

          - `include_thoughts?: boolean`

            Whether to include thoughts in the model's response.

          - `thinking_budget?: number`

            The thinking budget for the model.

      - `AzureModelSettings`

        Azure OpenAI model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "azure"`

          The type of the provider.

          - `"azure"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

      - `XaiModelSettings`

        xAI model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "xai"`

          The type of the provider.

          - `"xai"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

      - `MoonshotModelSettings`

        Moonshot/Kimi model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "moonshot"`

          The type of the provider.

          - `"moonshot"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `strict?: boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature?: number`

          The temperature of the model.

      - `ZaiModelSettings`

        Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "zai"`

          The type of the provider.

          - `"zai"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

        - `thinking?: Thinking`

          The thinking configuration for GLM-4.5+ models.

          - `clear_thinking?: boolean`

            If False, preserved thinking is used (recommended for agents).

          - `type?: "enabled" | "disabled"`

            Whether thinking is enabled or disabled.

            - `"enabled"`

            - `"disabled"`

      - `MoonshotCodingModelSettings`

        Kimi Code model configuration (Anthropic-compatible).

        - `effort?: "low" | "medium" | "high" | 2 more | null`

          Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

          - `"max"`

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "moonshot_coding"`

          The type of the provider.

          - `"moonshot_coding"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `strict?: boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature?: number`

          The temperature of the model.

        - `thinking?: Thinking`

          The thinking configuration for the model.

          - `budget_tokens?: number`

            The maximum number of tokens the model can use for extended thinking.

          - `type?: "enabled" | "disabled"`

            The type of thinking to use.

            - `"enabled"`

            - `"disabled"`

        - `verbosity?: "low" | "medium" | "high" | null`

          Soft control for how verbose model output should be, used for GPT-5 models.

          - `"low"`

          - `"medium"`

          - `"high"`

      - `GroqModelSettings`

        Groq model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "groq"`

          The type of the provider.

          - `"groq"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

      - `DeepseekModelSettings`

        Deepseek model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "deepseek"`

          The type of the provider.

          - `"deepseek"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

      - `TogetherModelSettings`

        Together AI model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "together"`

          The type of the provider.

          - `"together"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

      - `BedrockModelSettings`

        AWS Bedrock model configuration.

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "bedrock"`

          The type of the provider.

          - `"bedrock"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

      - `BasetenModelSettings`

        Baseten model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "baseten"`

          The type of the provider.

          - `"baseten"`

        - `temperature?: number`

          The temperature of the model.

      - `OpenRouterModelSettings`

        OpenRouter model configuration (OpenAI-compatible).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "openrouter"`

          The type of the provider.

          - `"openrouter"`

        - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

          The response format for the model.

          - `TextResponseFormat`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

        - `temperature?: number`

          The temperature of the model.

      - `ChatGptoAuthModelSettings`

        ChatGPT OAuth model configuration (uses ChatGPT backend API).

        - `max_output_tokens?: number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls?: boolean`

          Whether to enable parallel tool calling.

        - `provider_type?: "chatgpt_oauth"`

          The type of the provider.

          - `"chatgpt_oauth"`

        - `reasoning?: Reasoning`

          The reasoning configuration for the model.

          - `reasoning_effort?: "none" | "low" | "medium" | 2 more`

            The reasoning effort level for GPT-5.x and o-series models.

            - `"none"`

            - `"low"`

            - `"medium"`

            - `"high"`

            - `"xhigh"`

        - `temperature?: number`

          The temperature of the model.

    - `prompt?: string | null`

      The prompt to use for summarization. If None, uses mode-specific default.

    - `prompt_acknowledgement?: boolean`

      Whether to include an acknowledgement post-prompt (helps prevent non-summary outputs).

    - `sliding_window_percentage?: number`

      The percentage of the context window to keep post-summarization (only used in sliding window modes).

### Returns

- `ConversationRecompileResponse = string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.conversations.recompile('default');

console.log(response);
```

#### Response

```json
"string"
```
