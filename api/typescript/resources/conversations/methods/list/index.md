## List Conversations

`client.conversations.list(ConversationListParamsquery?, RequestOptionsoptions?): ConversationListResponse`

**get** `/v1/conversations/`

List all conversations for an agent (or all conversations if agent_id not provided).

### Parameters

- `query: ConversationListParams`

  - `after?: string | null`

    Cursor for pagination (conv ID). Returns results relative to this ID in the specified sort order. Expected format: 'conv-<uuid4>'

  - `agent_id?: string | null`

    The agent ID to list conversations for (optional - returns all conversations if not provided)

  - `archive_status?: "unarchived" | "archived" | "all"`

    Whether to return unarchived conversations only, archived conversations only, or all conversations

    - `"unarchived"`

    - `"archived"`

    - `"all"`

  - `limit?: number`

    Maximum number of conversations to return

  - `order?: "asc" | "desc"`

    Sort order for conversations. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at" | "last_run_completion" | "last_message_at"`

    Field to sort by

    - `"created_at"`

    - `"last_run_completion"`

    - `"last_message_at"`

  - `summary_search?: string | null`

    Search for text within conversation summaries

### Returns

- `ConversationListResponse = Array<Conversation>`

  - `id: string`

    The unique identifier of the conversation.

  - `agent_id: string`

    The ID of the agent this conversation belongs to.

  - `archived?: boolean`

    Whether the conversation is archived.

  - `archived_at?: string | null`

    Timestamp of when the conversation was archived.

  - `context_window_limit?: number | null`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at?: string | null`

    The timestamp when the object was created.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `description?: string | null`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids?: Array<string> | null`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at?: string | null`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `model?: string | null`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings?: OpenAIModelSettings | SgLangModelSettings | AnthropicModelSettings | 14 more | null`

    The model settings for this conversation (overrides agent's model settings).

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

  - `summary?: string | null`

    A summary of the conversation.

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const conversations = await client.conversations.list();

console.log(conversations);
```

#### Response

```json
[
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
]
```
