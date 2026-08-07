# Conversations

## Create Conversation

**post** `/v1/conversations/`

Create a new conversation for an agent.

### Query Parameters

- `agent_id: string`

  The agent ID to create a conversation for

### Body Parameters

- `context_window_limit: optional number`

  The context window limit for this conversation (overrides agent's context window).

- `description: optional string`

  A generated description of the conversation used for search and bootstrap context.

- `hidden: optional boolean`

  Whether the new conversation should be hidden from listings.

- `model: optional string`

  The model handle for this conversation (overrides agent's model). Format: provider/model-name.

- `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

  The model settings for this conversation (overrides agent's model settings).

  - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "openai"`

      The type of the provider.

      - `"openai"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

        The reasoning effort to use when generating text reasoning models

        - `"none"`

        - `"minimal"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

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

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

  - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

    SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "sglang"`

      The type of the provider.

      - `"sglang"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

        The reasoning effort to use when generating text reasoning models

        - `"none"`

        - `"minimal"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `tool_call_parser: optional string`

      SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

  - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

    - `effort: optional "low" or "medium" or "high" or 2 more`

      Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

      - `"low"`

      - `"medium"`

      - `"high"`

      - `"xhigh"`

      - `"max"`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "anthropic"`

      The type of the provider.

      - `"anthropic"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { budget_tokens, type }`

      The thinking configuration for the model.

      - `budget_tokens: optional number`

        The maximum number of tokens the model can use for extended thinking.

      - `type: optional "enabled" or "disabled"`

        The type of thinking to use.

        - `"enabled"`

        - `"disabled"`

    - `verbosity: optional "low" or "medium" or "high"`

      Soft control for how verbose model output should be, used for GPT-5 models.

      - `"low"`

      - `"medium"`

      - `"high"`

  - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "google_ai"`

      The type of the provider.

      - `"google_ai"`

    - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response schema for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking_config: optional object { include_thoughts, thinking_budget }`

      The thinking configuration for the model.

      - `include_thoughts: optional boolean`

        Whether to include thoughts in the model's response.

      - `thinking_budget: optional number`

        The thinking budget for the model.

  - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "google_vertex"`

      The type of the provider.

      - `"google_vertex"`

    - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response schema for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking_config: optional object { include_thoughts, thinking_budget }`

      The thinking configuration for the model.

      - `include_thoughts: optional boolean`

        Whether to include thoughts in the model's response.

      - `thinking_budget: optional number`

        The thinking budget for the model.

  - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Azure OpenAI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "azure"`

      The type of the provider.

      - `"azure"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    xAI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "xai"`

      The type of the provider.

      - `"xai"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    Moonshot/Kimi model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "moonshot"`

      The type of the provider.

      - `"moonshot"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

  - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "zai"`

      The type of the provider.

      - `"zai"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { clear_thinking, type }`

      The thinking configuration for GLM-4.5+ models.

      - `clear_thinking: optional boolean`

        If False, preserved thinking is used (recommended for agents).

      - `type: optional "enabled" or "disabled"`

        Whether thinking is enabled or disabled.

        - `"enabled"`

        - `"disabled"`

  - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

    Kimi Code model configuration (Anthropic-compatible).

    - `effort: optional "low" or "medium" or "high" or 2 more`

      Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

      - `"low"`

      - `"medium"`

      - `"high"`

      - `"xhigh"`

      - `"max"`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "moonshot_coding"`

      The type of the provider.

      - `"moonshot_coding"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { budget_tokens, type }`

      The thinking configuration for the model.

      - `budget_tokens: optional number`

        The maximum number of tokens the model can use for extended thinking.

      - `type: optional "enabled" or "disabled"`

        The type of thinking to use.

        - `"enabled"`

        - `"disabled"`

    - `verbosity: optional "low" or "medium" or "high"`

      Soft control for how verbose model output should be, used for GPT-5 models.

      - `"low"`

      - `"medium"`

      - `"high"`

  - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Groq model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "groq"`

      The type of the provider.

      - `"groq"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Deepseek model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "deepseek"`

      The type of the provider.

      - `"deepseek"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Together AI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "together"`

      The type of the provider.

      - `"together"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    AWS Bedrock model configuration.

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "bedrock"`

      The type of the provider.

      - `"bedrock"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

    Baseten model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "baseten"`

      The type of the provider.

      - `"baseten"`

    - `temperature: optional number`

      The temperature of the model.

  - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    OpenRouter model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "openrouter"`

      The type of the provider.

      - `"openrouter"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    ChatGPT OAuth model configuration (uses ChatGPT backend API).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "chatgpt_oauth"`

      The type of the provider.

      - `"chatgpt_oauth"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

        The reasoning effort level for GPT-5.x and o-series models.

        - `"none"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `temperature: optional number`

      The temperature of the model.

- `summary: optional string`

  A summary of the conversation.

### Returns

- `Conversation object { id, agent_id, archived, 12 more }`

  Represents a conversation on an agent for concurrent messaging.

  - `id: string`

    The unique identifier of the conversation.

  - `agent_id: string`

    The ID of the agent this conversation belongs to.

  - `archived: optional boolean`

    Whether the conversation is archived.

  - `archived_at: optional string`

    Timestamp of when the conversation was archived.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids: optional array of string`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at: optional string`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/conversations/ \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
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

## List Conversations

**get** `/v1/conversations/`

List all conversations for an agent (or all conversations if agent_id not provided).

### Query Parameters

- `after: optional string`

  Cursor for pagination (conv ID). Returns results relative to this ID in the specified sort order. Expected format: 'conv-<uuid4>'

- `agent_id: optional string`

  The agent ID to list conversations for (optional - returns all conversations if not provided)

- `archive_status: optional "unarchived" or "archived" or "all"`

  Whether to return unarchived conversations only, archived conversations only, or all conversations

  - `"unarchived"`

  - `"archived"`

  - `"all"`

- `limit: optional number`

  Maximum number of conversations to return

- `order: optional "asc" or "desc"`

  Sort order for conversations. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at" or "last_run_completion" or "last_message_at"`

  Field to sort by

  - `"created_at"`

  - `"last_run_completion"`

  - `"last_message_at"`

- `summary_search: optional string`

  Search for text within conversation summaries

### Returns

- `id: string`

  The unique identifier of the conversation.

- `agent_id: string`

  The ID of the agent this conversation belongs to.

- `archived: optional boolean`

  Whether the conversation is archived.

- `archived_at: optional string`

  Timestamp of when the conversation was archived.

- `context_window_limit: optional number`

  The context window limit for this conversation (overrides agent's context window).

- `created_at: optional string`

  The timestamp when the object was created.

- `created_by_id: optional string`

  The id of the user that made this object.

- `description: optional string`

  A generated description of the conversation used for search and bootstrap context.

- `in_context_message_ids: optional array of string`

  The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

- `last_message_at: optional string`

  Timestamp of the most recent message request sent to this conversation.

- `last_updated_by_id: optional string`

  The id of the user that made this object.

- `model: optional string`

  The model handle for this conversation (overrides agent's model). Format: provider/model-name.

- `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

  The model settings for this conversation (overrides agent's model settings).

  - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "openai"`

      The type of the provider.

      - `"openai"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

        The reasoning effort to use when generating text reasoning models

        - `"none"`

        - `"minimal"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

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

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

  - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

    SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "sglang"`

      The type of the provider.

      - `"sglang"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

        The reasoning effort to use when generating text reasoning models

        - `"none"`

        - `"minimal"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `tool_call_parser: optional string`

      SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

  - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

    - `effort: optional "low" or "medium" or "high" or 2 more`

      Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

      - `"low"`

      - `"medium"`

      - `"high"`

      - `"xhigh"`

      - `"max"`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "anthropic"`

      The type of the provider.

      - `"anthropic"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { budget_tokens, type }`

      The thinking configuration for the model.

      - `budget_tokens: optional number`

        The maximum number of tokens the model can use for extended thinking.

      - `type: optional "enabled" or "disabled"`

        The type of thinking to use.

        - `"enabled"`

        - `"disabled"`

    - `verbosity: optional "low" or "medium" or "high"`

      Soft control for how verbose model output should be, used for GPT-5 models.

      - `"low"`

      - `"medium"`

      - `"high"`

  - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "google_ai"`

      The type of the provider.

      - `"google_ai"`

    - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response schema for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking_config: optional object { include_thoughts, thinking_budget }`

      The thinking configuration for the model.

      - `include_thoughts: optional boolean`

        Whether to include thoughts in the model's response.

      - `thinking_budget: optional number`

        The thinking budget for the model.

  - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "google_vertex"`

      The type of the provider.

      - `"google_vertex"`

    - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response schema for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking_config: optional object { include_thoughts, thinking_budget }`

      The thinking configuration for the model.

      - `include_thoughts: optional boolean`

        Whether to include thoughts in the model's response.

      - `thinking_budget: optional number`

        The thinking budget for the model.

  - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Azure OpenAI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "azure"`

      The type of the provider.

      - `"azure"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    xAI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "xai"`

      The type of the provider.

      - `"xai"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    Moonshot/Kimi model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "moonshot"`

      The type of the provider.

      - `"moonshot"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

  - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "zai"`

      The type of the provider.

      - `"zai"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { clear_thinking, type }`

      The thinking configuration for GLM-4.5+ models.

      - `clear_thinking: optional boolean`

        If False, preserved thinking is used (recommended for agents).

      - `type: optional "enabled" or "disabled"`

        Whether thinking is enabled or disabled.

        - `"enabled"`

        - `"disabled"`

  - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

    Kimi Code model configuration (Anthropic-compatible).

    - `effort: optional "low" or "medium" or "high" or 2 more`

      Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

      - `"low"`

      - `"medium"`

      - `"high"`

      - `"xhigh"`

      - `"max"`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "moonshot_coding"`

      The type of the provider.

      - `"moonshot_coding"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { budget_tokens, type }`

      The thinking configuration for the model.

      - `budget_tokens: optional number`

        The maximum number of tokens the model can use for extended thinking.

      - `type: optional "enabled" or "disabled"`

        The type of thinking to use.

        - `"enabled"`

        - `"disabled"`

    - `verbosity: optional "low" or "medium" or "high"`

      Soft control for how verbose model output should be, used for GPT-5 models.

      - `"low"`

      - `"medium"`

      - `"high"`

  - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Groq model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "groq"`

      The type of the provider.

      - `"groq"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Deepseek model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "deepseek"`

      The type of the provider.

      - `"deepseek"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Together AI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "together"`

      The type of the provider.

      - `"together"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    AWS Bedrock model configuration.

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "bedrock"`

      The type of the provider.

      - `"bedrock"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

    Baseten model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "baseten"`

      The type of the provider.

      - `"baseten"`

    - `temperature: optional number`

      The temperature of the model.

  - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    OpenRouter model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "openrouter"`

      The type of the provider.

      - `"openrouter"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    ChatGPT OAuth model configuration (uses ChatGPT backend API).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "chatgpt_oauth"`

      The type of the provider.

      - `"chatgpt_oauth"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

        The reasoning effort level for GPT-5.x and o-series models.

        - `"none"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `temperature: optional number`

      The temperature of the model.

- `summary: optional string`

  A summary of the conversation.

- `updated_at: optional string`

  The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/conversations/ \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

## Retrieve Conversation

**get** `/v1/conversations/{conversation_id}`

Retrieve a specific conversation.

### Path Parameters

- `conversation_id: string`

  The ID of the conv in the format 'conv-<uuid4>'

### Returns

- `Conversation object { id, agent_id, archived, 12 more }`

  Represents a conversation on an agent for concurrent messaging.

  - `id: string`

    The unique identifier of the conversation.

  - `agent_id: string`

    The ID of the agent this conversation belongs to.

  - `archived: optional boolean`

    Whether the conversation is archived.

  - `archived_at: optional string`

    Timestamp of when the conversation was archived.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids: optional array of string`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at: optional string`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

## Update Conversation

**patch** `/v1/conversations/{conversation_id}`

Update a conversation.

### Path Parameters

- `conversation_id: string`

  The ID of the conv in the format 'conv-<uuid4>'

### Body Parameters

- `archived: optional boolean`

  Whether the conversation is archived.

- `context_window_limit: optional number`

  The context window limit for this conversation (overrides agent's context window).

- `description: optional string`

  A generated description of the conversation used for search and bootstrap context.

- `last_message_at: optional string`

  Timestamp of the most recent message request sent to this conversation.

- `model: optional string`

  The model handle for this conversation (overrides agent's model). Format: provider/model-name.

- `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

  The model settings for this conversation (overrides agent's model settings).

  - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "openai"`

      The type of the provider.

      - `"openai"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

        The reasoning effort to use when generating text reasoning models

        - `"none"`

        - `"minimal"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

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

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

  - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

    SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "sglang"`

      The type of the provider.

      - `"sglang"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

        The reasoning effort to use when generating text reasoning models

        - `"none"`

        - `"minimal"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `tool_call_parser: optional string`

      SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

  - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

    - `effort: optional "low" or "medium" or "high" or 2 more`

      Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

      - `"low"`

      - `"medium"`

      - `"high"`

      - `"xhigh"`

      - `"max"`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "anthropic"`

      The type of the provider.

      - `"anthropic"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { budget_tokens, type }`

      The thinking configuration for the model.

      - `budget_tokens: optional number`

        The maximum number of tokens the model can use for extended thinking.

      - `type: optional "enabled" or "disabled"`

        The type of thinking to use.

        - `"enabled"`

        - `"disabled"`

    - `verbosity: optional "low" or "medium" or "high"`

      Soft control for how verbose model output should be, used for GPT-5 models.

      - `"low"`

      - `"medium"`

      - `"high"`

  - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "google_ai"`

      The type of the provider.

      - `"google_ai"`

    - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response schema for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking_config: optional object { include_thoughts, thinking_budget }`

      The thinking configuration for the model.

      - `include_thoughts: optional boolean`

        Whether to include thoughts in the model's response.

      - `thinking_budget: optional number`

        The thinking budget for the model.

  - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "google_vertex"`

      The type of the provider.

      - `"google_vertex"`

    - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response schema for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking_config: optional object { include_thoughts, thinking_budget }`

      The thinking configuration for the model.

      - `include_thoughts: optional boolean`

        Whether to include thoughts in the model's response.

      - `thinking_budget: optional number`

        The thinking budget for the model.

  - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Azure OpenAI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "azure"`

      The type of the provider.

      - `"azure"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    xAI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "xai"`

      The type of the provider.

      - `"xai"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    Moonshot/Kimi model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "moonshot"`

      The type of the provider.

      - `"moonshot"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

  - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

    Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "zai"`

      The type of the provider.

      - `"zai"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { clear_thinking, type }`

      The thinking configuration for GLM-4.5+ models.

      - `clear_thinking: optional boolean`

        If False, preserved thinking is used (recommended for agents).

      - `type: optional "enabled" or "disabled"`

        Whether thinking is enabled or disabled.

        - `"enabled"`

        - `"disabled"`

  - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

    Kimi Code model configuration (Anthropic-compatible).

    - `effort: optional "low" or "medium" or "high" or 2 more`

      Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

      - `"low"`

      - `"medium"`

      - `"high"`

      - `"xhigh"`

      - `"max"`

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "moonshot_coding"`

      The type of the provider.

      - `"moonshot_coding"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `strict: optional boolean`

      Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

    - `temperature: optional number`

      The temperature of the model.

    - `thinking: optional object { budget_tokens, type }`

      The thinking configuration for the model.

      - `budget_tokens: optional number`

        The maximum number of tokens the model can use for extended thinking.

      - `type: optional "enabled" or "disabled"`

        The type of thinking to use.

        - `"enabled"`

        - `"disabled"`

    - `verbosity: optional "low" or "medium" or "high"`

      Soft control for how verbose model output should be, used for GPT-5 models.

      - `"low"`

      - `"medium"`

      - `"high"`

  - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Groq model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "groq"`

      The type of the provider.

      - `"groq"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Deepseek model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "deepseek"`

      The type of the provider.

      - `"deepseek"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Together AI model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "together"`

      The type of the provider.

      - `"together"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    AWS Bedrock model configuration.

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "bedrock"`

      The type of the provider.

      - `"bedrock"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

    Baseten model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "baseten"`

      The type of the provider.

      - `"baseten"`

    - `temperature: optional number`

      The temperature of the model.

  - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    OpenRouter model configuration (OpenAI-compatible).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "openrouter"`

      The type of the provider.

      - `"openrouter"`

    - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

      The response format for the model.

      - `TextResponseFormat object { type }`

        Response format for plain text responses.

      - `JsonSchemaResponseFormat object { json_schema, type }`

        Response format for JSON schema-based responses.

      - `JsonObjectResponseFormat object { type }`

        Response format for JSON object responses.

    - `temperature: optional number`

      The temperature of the model.

  - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    ChatGPT OAuth model configuration (uses ChatGPT backend API).

    - `max_output_tokens: optional number`

      The maximum number of tokens the model can generate.

    - `parallel_tool_calls: optional boolean`

      Whether to enable parallel tool calling.

    - `provider_type: optional "chatgpt_oauth"`

      The type of the provider.

      - `"chatgpt_oauth"`

    - `reasoning: optional object { reasoning_effort }`

      The reasoning configuration for the model.

      - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

        The reasoning effort level for GPT-5.x and o-series models.

        - `"none"`

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

    - `temperature: optional number`

      The temperature of the model.

- `summary: optional string`

  A summary of the conversation.

### Returns

- `Conversation object { id, agent_id, archived, 12 more }`

  Represents a conversation on an agent for concurrent messaging.

  - `id: string`

    The unique identifier of the conversation.

  - `agent_id: string`

    The ID of the agent this conversation belongs to.

  - `archived: optional boolean`

    Whether the conversation is archived.

  - `archived_at: optional string`

    Timestamp of when the conversation was archived.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids: optional array of string`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at: optional string`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID \
    -X PATCH \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
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

## Delete Conversation

**delete** `/v1/conversations/{conversation_id}`

Delete a conversation.

The conversation will no longer appear in list operations.

### Path Parameters

- `conversation_id: string`

  The ID of the conv in the format 'conv-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID \
    -X DELETE \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## Cancel Conversation

**post** `/v1/conversations/{conversation_id}/cancel`

Cancel runs associated with a conversation.

Note: To cancel active runs, Redis is required.

**Agent-direct mode**: Pass conversation_id="default" with agent_id query parameter
to cancel runs for the agent's default conversation.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Query Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/cancel \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "foo": "bar"
}
```

## Recompile Conversation

**post** `/v1/conversations/{conversation_id}/recompile`

Manually trigger system prompt recompilation for a conversation.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Query Parameters

- `dry_run: optional boolean`

  If True, do not persist changes; still returns the compiled system prompt.

### Body Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `compaction_settings: optional object { clip_chars, mode, model, 4 more }`

  Configuration for conversation compaction / summarization.

  Per-model settings (temperature,
  max tokens, etc.) are derived from the default configuration for that handle.

  - `clip_chars: optional number`

    The maximum length of the summary in characters. If none, no clipping is performed.

  - `mode: optional "all" or "sliding_window" or "self_compact_all" or "self_compact_sliding_window"`

    The type of summarization technique use.

    - `"all"`

    - `"sliding_window"`

    - `"self_compact_all"`

    - `"self_compact_sliding_window"`

  - `model: optional string`

    Model handle to use for sliding_window/all summarization (format: provider/model-name). If None, uses lightweight provider-specific defaults.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    Optional model settings used to override defaults for the summarizer model.

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `prompt: optional string`

    The prompt to use for summarization. If None, uses mode-specific default.

  - `prompt_acknowledgement: optional boolean`

    Whether to include an acknowledgement post-prompt (helps prevent non-summary outputs).

  - `sliding_window_percentage: optional number`

    The percentage of the context window to keep post-summarization (only used in sliding window modes).

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/recompile \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
"string"
```

## Fork Conversation

**post** `/v1/conversations/{conversation_id}/fork`

Fork an existing conversation.

Creates a new conversation that shares the same in-context messages as the source
conversation, but with a newly compiled system message reflecting the latest memory
block values. The forked conversation belongs to the same agent as the source.

If message_id is provided, only source in-context messages up to and including
that message are included in the fork.

**Agent-direct mode**: Pass conversation_id="default" with agent_id query parameter
to fork the agent's default (agent-direct) message history into a new conversation.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Query Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation

- `hidden: optional boolean`

  Whether the forked conversation should be hidden from listings

- `message_id: optional string`

  The ID of the message in the format 'message-<uuid4>'

### Returns

- `Conversation object { id, agent_id, archived, 12 more }`

  Represents a conversation on an agent for concurrent messaging.

  - `id: string`

    The unique identifier of the conversation.

  - `agent_id: string`

    The ID of the agent this conversation belongs to.

  - `archived: optional boolean`

    Whether the conversation is archived.

  - `archived_at: optional string`

    Timestamp of when the conversation was archived.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids: optional array of string`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at: optional string`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/fork \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

## Domain Types

### Conversation

- `Conversation object { id, agent_id, archived, 12 more }`

  Represents a conversation on an agent for concurrent messaging.

  - `id: string`

    The unique identifier of the conversation.

  - `agent_id: string`

    The ID of the agent this conversation belongs to.

  - `archived: optional boolean`

    Whether the conversation is archived.

  - `archived_at: optional string`

    Timestamp of when the conversation was archived.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids: optional array of string`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at: optional string`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Create Conversation

- `CreateConversation object { context_window_limit, description, hidden, 3 more }`

  Request model for creating a new conversation.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `hidden: optional boolean`

    Whether the new conversation should be hidden from listings.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

### Update Conversation

- `UpdateConversation object { archived, context_window_limit, description, 4 more }`

  Request model for updating a conversation.

  - `archived: optional boolean`

    Whether the conversation is archived.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `last_message_at: optional string`

    Timestamp of the most recent message request sent to this conversation.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

### Conversation List Response

- `ConversationListResponse = array of Conversation`

  - `id: string`

    The unique identifier of the conversation.

  - `agent_id: string`

    The ID of the agent this conversation belongs to.

  - `archived: optional boolean`

    Whether the conversation is archived.

  - `archived_at: optional string`

    Timestamp of when the conversation was archived.

  - `context_window_limit: optional number`

    The context window limit for this conversation (overrides agent's context window).

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    A generated description of the conversation used for search and bootstrap context.

  - `in_context_message_ids: optional array of string`

    The IDs of in-context messages for the conversation. Null means this field was not retrieved/hydrated for this response.

  - `last_message_at: optional string`

    Timestamp of the most recent message request sent to this conversation.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `model: optional string`

    The model handle for this conversation (overrides agent's model). Format: provider/model-name.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    The model settings for this conversation (overrides agent's model settings).

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `summary: optional string`

    A summary of the conversation.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Conversation Delete Response

- `ConversationDeleteResponse = unknown`

### Conversation Cancel Response

- `ConversationCancelResponse = map[unknown]`

### Conversation Recompile Response

- `ConversationRecompileResponse = string`

# Messages

## List Conversation Messages

**get** `/v1/conversations/{conversation_id}/messages`

List all messages in a conversation.

Returns LettaMessage objects (UserMessage, AssistantMessage, etc.) for all
messages in the conversation, with support for cursor-based pagination.

**Agent-direct mode**: Pass conversation_id="default" with agent_id parameter
to list messages from the agent's default conversation.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Query Parameters

- `after: optional string`

  Cursor for pagination (message ID). Returns results relative to this ID in the specified sort order. Expected format: 'message-<uuid4>'

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation

- `before: optional string`

  Cursor for pagination (message ID). Returns results relative to this ID in the specified sort order. Expected format: 'message-<uuid4>'

- `group_id: optional string`

  Group ID to filter messages by.

- `include_err: optional boolean`

  Whether to include error messages and error statuses. For debugging purposes only.

- `include_return_message_types: optional array of MessageType`

  Message types to include in response. When null, all message types are returned.

  - `"system_message"`

  - `"user_message"`

  - `"assistant_message"`

  - `"reasoning_message"`

  - `"hidden_reasoning_message"`

  - `"tool_call_message"`

  - `"tool_return_message"`

  - `"approval_request_message"`

  - `"approval_response_message"`

  - `"summary_message"`

  - `"event_message"`

- `limit: optional number`

  Maximum number of messages to return

- `order: optional "asc" or "desc"`

  Sort order for messages by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

### Returns

- `SystemMessage object { id, content, date, 8 more }`

  A message generated by the system. Never streamed back on a response, only used for cursor pagination.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  content (str): The message content sent by the system

  - `id: string`

  - `content: string`

    The message content sent by the system

  - `date: string`

  - `is_err: optional boolean`

  - `message_type: optional "system_message"`

    The type of the message.

    - `"system_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

- `UserMessage object { id, content, date, 8 more }`

  A message sent by the user. Never streamed back on a response, only used for cursor pagination.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  content (Union[str, List[LettaUserMessageContentUnion]]): The message content sent by the user (can be a string or an array of multi-modal content parts)

  - `id: string`

  - `content: array of LettaUserMessageContentUnion or string`

    The message content sent by the user (can be a string or an array of multi-modal content parts)

    - `array of LettaUserMessageContentUnion`

      - `TextContent object { text, signature, type }`

        - `text: string`

          The text content of the message.

        - `signature: optional string`

          Stores a unique identifier for any reasoning associated with this text content.

        - `type: optional "text"`

          The type of the message.

          - `"text"`

      - `ImageContent object { source, type }`

        - `source: object { url, type }  or object { data, media_type, detail, type }  or object { file_id, data, detail, 2 more }`

          The source of the image.

          - `URL object { url, type }`

            - `url: string`

              The URL of the image.

            - `type: optional "url"`

              The source type for the image.

              - `"url"`

          - `Base64 object { data, media_type, detail, type }`

            - `data: string`

              The base64 encoded image data.

            - `media_type: string`

              The media type for the image.

            - `detail: optional string`

              What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

            - `type: optional "base64"`

              The source type for the image.

              - `"base64"`

          - `Letta object { file_id, data, detail, 2 more }`

            - `file_id: string`

              The unique identifier of the image file persisted in storage.

            - `data: optional string`

              The base64 encoded image data.

            - `detail: optional string`

              What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

            - `media_type: optional string`

              The media type for the image.

            - `type: optional "letta"`

              The source type for the image.

              - `"letta"`

        - `type: optional "image"`

          The type of the message.

          - `"image"`

    - `string`

  - `date: string`

  - `is_err: optional boolean`

  - `message_type: optional "user_message"`

    The type of the message.

    - `"user_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

- `ReasoningMessage object { id, date, reasoning, 10 more }`

  Representation of an agent's internal reasoning.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  source (Literal["reasoner_model", "non_reasoner_model"]): Whether the reasoning
  content was generated natively by a reasoner model or derived via prompting
  reasoning (str): The internal reasoning of the agent
  signature (Optional[str]): The model-generated signature of the reasoning step

  - `id: string`

  - `date: string`

  - `reasoning: string`

  - `is_err: optional boolean`

  - `message_type: optional "reasoning_message"`

    The type of the message.

    - `"reasoning_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `signature: optional string`

  - `source: optional "reasoner_model" or "non_reasoner_model"`

    - `"reasoner_model"`

    - `"non_reasoner_model"`

  - `step_id: optional string`

- `HiddenReasoningMessage object { id, date, state, 9 more }`

  Representation of an agent's internal reasoning where reasoning content
  has been hidden from the response.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  state (Literal["redacted", "omitted"]): Whether the reasoning
  content was redacted by the provider or simply omitted by the API
  hidden_reasoning (Optional[str]): The internal reasoning of the agent

  - `id: string`

  - `date: string`

  - `state: "redacted" or "omitted"`

    - `"redacted"`

    - `"omitted"`

  - `hidden_reasoning: optional string`

  - `is_err: optional boolean`

  - `message_type: optional "hidden_reasoning_message"`

    The type of the message.

    - `"hidden_reasoning_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

- `ToolCallMessage object { id, date, tool_call, 9 more }`

  A message representing a request to call a tool (generated by the LLM to trigger tool execution).

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  tool_call (Union[ToolCall, ToolCallDelta]): The tool call

  - `id: string`

  - `date: string`

  - `tool_call: ToolCall or ToolCallDelta`

    - `ToolCall object { arguments, name, tool_call_id }`

      - `arguments: string`

      - `name: string`

      - `tool_call_id: string`

    - `ToolCallDelta object { arguments, name, tool_call_id }`

      - `arguments: optional string`

      - `name: optional string`

      - `tool_call_id: optional string`

  - `is_err: optional boolean`

  - `message_type: optional "tool_call_message"`

    The type of the message.

    - `"tool_call_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

  - `tool_calls: optional array of ToolCall or ToolCallDelta`

    - `array of ToolCall`

      - `arguments: string`

      - `name: string`

      - `tool_call_id: string`

    - `ToolCallDelta object { arguments, name, tool_call_id }`

- `ToolReturnMessage object { id, date, status, 13 more }`

  A message representing the return value of a tool call (generated by Letta executing the requested tool).

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  tool_return (str): The return value of the tool (deprecated, use tool_returns)
  status (Literal["success", "error"]): The status of the tool call (deprecated, use tool_returns)
  tool_call_id (str): A unique identifier for the tool call that generated this message (deprecated, use tool_returns)
  stdout (Optional[List(str)]): Captured stdout (e.g. prints, logs) from the tool invocation (deprecated, use tool_returns)
  stderr (Optional[List(str)]): Captured stderr from the tool invocation (deprecated, use tool_returns)
  tool_returns (Optional[List[ToolReturn]]): List of tool returns for multi-tool support

  - `id: string`

  - `date: string`

  - `status: "success" or "error"`

    - `"success"`

    - `"error"`

  - `tool_call_id: string`

  - `tool_return: string`

  - `is_err: optional boolean`

  - `message_type: optional "tool_return_message"`

    The type of the message.

    - `"tool_return_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `stderr: optional array of string`

  - `stdout: optional array of string`

  - `step_id: optional string`

  - `tool_returns: optional array of ToolReturn`

    - `status: "success" or "error"`

      - `"success"`

      - `"error"`

    - `tool_call_id: string`

    - `tool_return: array of TextContent or ImageContent or string`

      The tool return value - either a string or list of content parts (text/image)

      - `array of TextContent or ImageContent`

        - `TextContent object { text, signature, type }`

        - `ImageContent object { source, type }`

      - `string`

    - `stderr: optional array of string`

    - `stdout: optional array of string`

    - `type: optional "tool"`

      The message type to be created.

      - `"tool"`

- `AssistantMessage object { id, content, date, 8 more }`

  A message sent by the LLM in response to user input. Used in the LLM context.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  content (Union[str, List[LettaAssistantMessageContentUnion]]): The message content sent by the agent (can be a string or an array of content parts)

  - `id: string`

  - `content: array of LettaAssistantMessageContentUnion or string`

    The message content sent by the agent (can be a string or an array of content parts)

    - `array of LettaAssistantMessageContentUnion`

      - `text: string`

        The text content of the message.

      - `signature: optional string`

        Stores a unique identifier for any reasoning associated with this text content.

      - `type: optional "text"`

        The type of the message.

        - `"text"`

    - `string`

  - `date: string`

  - `is_err: optional boolean`

  - `message_type: optional "assistant_message"`

    The type of the message.

    - `"assistant_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

- `ApprovalRequestMessage object { id, date, tool_call, 9 more }`

  A message representing a request for approval to call a tool (generated by the LLM to trigger tool execution).

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  tool_call (ToolCall): The tool call

  - `id: string`

  - `date: string`

  - `tool_call: ToolCall or ToolCallDelta`

    The tool call that has been requested by the llm to run

    - `ToolCall object { arguments, name, tool_call_id }`

    - `ToolCallDelta object { arguments, name, tool_call_id }`

  - `is_err: optional boolean`

  - `message_type: optional "approval_request_message"`

    The type of the message.

    - `"approval_request_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

  - `tool_calls: optional array of ToolCall or ToolCallDelta`

    The tool calls that have been requested by the llm to run, which are pending approval

    - `array of ToolCall`

      - `arguments: string`

      - `name: string`

      - `tool_call_id: string`

    - `ToolCallDelta object { arguments, name, tool_call_id }`

- `ApprovalResponseMessage object { id, date, approval_request_id, 11 more }`

  A message representing a response form the user indicating whether a tool has been approved to run.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  approve: (bool) Whether the tool has been approved
  approval_request_id: The ID of the approval request
  reason: (Optional[str]) An optional explanation for the provided approval status

  - `id: string`

  - `date: string`

  - `approval_request_id: optional string`

    The message ID of the approval request

  - `approvals: optional array of ApprovalReturn or ToolReturn`

    The list of approval responses

    - `ApprovalReturn object { approve, tool_call_id, reason, type }`

      - `approve: boolean`

        Whether the tool has been approved

      - `tool_call_id: string`

        The ID of the tool call that corresponds to this approval

      - `reason: optional string`

        An optional explanation for the provided approval status

      - `type: optional "approval"`

        The message type to be created.

        - `"approval"`

    - `ToolReturn object { status, tool_call_id, tool_return, 3 more }`

      - `status: "success" or "error"`

      - `tool_call_id: string`

      - `tool_return: array of TextContent or ImageContent or string`

        The tool return value - either a string or list of content parts (text/image)

      - `stderr: optional array of string`

      - `stdout: optional array of string`

      - `type: optional "tool"`

        The message type to be created.

  - `approve: optional boolean`

    Whether the tool has been approved

  - `is_err: optional boolean`

  - `message_type: optional "approval_response_message"`

    The type of the message.

    - `"approval_response_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `reason: optional string`

    An optional explanation for the provided approval status

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

- `SummaryMessage object { id, date, summary, 9 more }`

  A message representing a summary of the conversation. Sent to the LLM as a user or system message depending on the provider.

  - `id: string`

  - `date: string`

  - `summary: string`

  - `compaction_stats: optional object { context_window, messages_count_after, messages_count_before, 3 more }`

    Statistics about a memory compaction operation.

    - `context_window: number`

      The model's context window size

    - `messages_count_after: number`

      Number of messages after compaction

    - `messages_count_before: number`

      Number of messages before compaction

    - `trigger: string`

      What triggered the compaction (e.g., 'context_window_exceeded', 'post_step_context_check')

    - `context_tokens_after: optional number`

      Token count after compaction (message tokens only, does not include tool definitions)

    - `context_tokens_before: optional number`

      Token count before compaction (from LLM usage stats, includes full context sent to LLM)

  - `is_err: optional boolean`

  - `message_type: optional "summary_message"`

    - `"summary_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

- `EventMessage object { id, date, event_data, 9 more }`

  A message for notifying the developer that an event that has occured (e.g. a compaction). Events are NOT part of the context window.

  - `id: string`

  - `date: string`

  - `event_data: map[unknown]`

  - `event_type: "compaction"`

    - `"compaction"`

  - `is_err: optional boolean`

  - `message_type: optional "event_message"`

    - `"event_message"`

  - `name: optional string`

  - `otid: optional string`

    The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

  - `run_id: optional string`

  - `sender_id: optional string`

  - `seq_id: optional number`

  - `step_id: optional string`

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/messages \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  {
    "id": "id",
    "content": "content",
    "date": "2019-12-27T18:11:19.117Z",
    "is_err": true,
    "message_type": "system_message",
    "name": "name",
    "otid": "otid",
    "run_id": "run_id",
    "sender_id": "sender_id",
    "seq_id": 0,
    "step_id": "step_id"
  }
]
```

## Send Conversation Message

**post** `/v1/conversations/{conversation_id}/messages`

Send a message to a conversation and get a response.

This endpoint sends a message to an existing conversation.
By default (streaming=true), returns a streaming response (Server-Sent Events).
Set streaming=false to get a complete JSON response.

**Agent-direct mode**: Pass conversation_id="default" with agent_id in request body
to send messages to the agent's default conversation with locking.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Body Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `assistant_message_tool_kwarg: optional string`

  The name of the message argument in the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

- `assistant_message_tool_name: optional string`

  The name of the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

- `background: optional boolean`

  Whether to process the request in the background (only used when streaming=true).

- `client_skills: optional array of object { description, location, name }`

  Client-side skills available in the environment. These are rendered in the system prompt's available skills section alongside agent-scoped skills from MemFS.

  - `description: string`

    Description of what the skill does

  - `location: string`

    Path or location hint for the skill (e.g. skills/my-skill/SKILL.md)

  - `name: string`

    The name of the skill

- `client_tools: optional array of object { name, description, parameters }`

  Client-side tools that the agent can call. When the agent calls a client-side tool, execution pauses and returns control to the client to execute the tool and provide the result via a ToolReturn.

  - `name: string`

    The name of the tool function

  - `description: optional string`

    Description of what the tool does

  - `parameters: optional map[unknown]`

    JSON Schema for the function parameters

- `enable_thinking: optional string`

  If set to True, enables reasoning before responses or tool calls from the agent.

- `include_compaction_messages: optional boolean`

  If True, compaction events emit structured `SummaryMessage` and `EventMessage` types. If False (default), compaction messages are not included in the response.

- `include_pings: optional boolean`

  Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts (only used when streaming=true).

- `include_return_message_types: optional array of MessageType`

  Only return specified message types in the response. If `None` (default) returns all messages.

  - `"system_message"`

  - `"user_message"`

  - `"assistant_message"`

  - `"reasoning_message"`

  - `"hidden_reasoning_message"`

  - `"tool_call_message"`

  - `"tool_return_message"`

  - `"approval_request_message"`

  - `"approval_response_message"`

  - `"summary_message"`

  - `"event_message"`

- `input: optional string or array of TextContent or ImageContent or ToolCallContent or 5 more`

  Syntactic sugar for a single user message. Equivalent to messages=[{'role': 'user', 'content': input}].

  - `string`

  - `array of TextContent or ImageContent or ToolCallContent or 5 more`

    - `TextContent object { text, signature, type }`

      - `text: string`

        The text content of the message.

      - `signature: optional string`

        Stores a unique identifier for any reasoning associated with this text content.

      - `type: optional "text"`

        The type of the message.

        - `"text"`

    - `ImageContent object { source, type }`

      - `source: object { url, type }  or object { data, media_type, detail, type }  or object { file_id, data, detail, 2 more }`

        The source of the image.

        - `URL object { url, type }`

          - `url: string`

            The URL of the image.

          - `type: optional "url"`

            The source type for the image.

            - `"url"`

        - `Base64 object { data, media_type, detail, type }`

          - `data: string`

            The base64 encoded image data.

          - `media_type: string`

            The media type for the image.

          - `detail: optional string`

            What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

          - `type: optional "base64"`

            The source type for the image.

            - `"base64"`

        - `Letta object { file_id, data, detail, 2 more }`

          - `file_id: string`

            The unique identifier of the image file persisted in storage.

          - `data: optional string`

            The base64 encoded image data.

          - `detail: optional string`

            What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

          - `media_type: optional string`

            The media type for the image.

          - `type: optional "letta"`

            The source type for the image.

            - `"letta"`

      - `type: optional "image"`

        The type of the message.

        - `"image"`

    - `ToolCallContent object { id, input, name, 2 more }`

      - `id: string`

        A unique identifier for this specific tool call instance.

      - `input: map[unknown]`

        The parameters being passed to the tool, structured as a dictionary of parameter names to values.

      - `name: string`

        The name of the tool being called.

      - `signature: optional string`

        Stores a unique identifier for any reasoning associated with this tool call.

      - `type: optional "tool_call"`

        Indicates this content represents a tool call event.

        - `"tool_call"`

    - `ToolReturnContent object { content, is_error, tool_call_id, type }`

      - `content: string`

        The content returned by the tool execution.

      - `is_error: boolean`

        Indicates whether the tool execution resulted in an error.

      - `tool_call_id: string`

        References the ID of the ToolCallContent that initiated this tool call.

      - `type: optional "tool_return"`

        Indicates this content represents a tool return event.

        - `"tool_return"`

    - `ReasoningContent object { is_native, reasoning, signature, type }`

      Sent via the Anthropic Messages API

      - `is_native: boolean`

        Whether the reasoning content was generated by a reasoner model that processed this step.

      - `reasoning: string`

        The intermediate reasoning or thought process content.

      - `signature: optional string`

        A unique identifier for this reasoning step.

      - `type: optional "reasoning"`

        Indicates this is a reasoning/intermediate step.

        - `"reasoning"`

    - `RedactedReasoningContent object { data, type }`

      Sent via the Anthropic Messages API

      - `data: string`

        The redacted or filtered intermediate reasoning content.

      - `type: optional "redacted_reasoning"`

        Indicates this is a redacted thinking step.

        - `"redacted_reasoning"`

    - `OmittedReasoningContent object { signature, type }`

      A placeholder for reasoning content we know is present, but isn't returned by the provider (e.g. OpenAI GPT-5 on ChatCompletions)

      - `signature: optional string`

        A unique identifier for this reasoning step.

      - `type: optional "omitted_reasoning"`

        Indicates this is an omitted reasoning step.

        - `"omitted_reasoning"`

    - `SummarizedReasoning object { id, summary, encrypted_content, type }`

      The style of reasoning content returned by the OpenAI Responses API

      - `id: string`

        The unique identifier for this reasoning step.

      - `summary: array of object { index, text }`

        Summaries of the reasoning content.

        - `index: number`

          The index of the summary part.

        - `text: string`

          The text of the summary part.

      - `encrypted_content: optional string`

        The encrypted reasoning content.

      - `type: optional "summarized_reasoning"`

        Indicates this is a summarized reasoning step.

        - `"summarized_reasoning"`

- `max_steps: optional number`

  Maximum number of steps the agent should take to process the request.

- `messages: optional array of MessageCreate or ApprovalCreate or object { tool_returns, group_id, otid, type }`

  The messages to be sent to the agent.

  - `MessageCreate object { content, role, batch_item_id, 5 more }`

    Request to create a message

    - `content: array of LettaMessageContentUnion or string`

      The content of the message.

      - `array of LettaMessageContentUnion`

        - `TextContent object { text, signature, type }`

        - `ImageContent object { source, type }`

        - `ToolCallContent object { id, input, name, 2 more }`

        - `ToolReturnContent object { content, is_error, tool_call_id, type }`

        - `ReasoningContent object { is_native, reasoning, signature, type }`

          Sent via the Anthropic Messages API

        - `RedactedReasoningContent object { data, type }`

          Sent via the Anthropic Messages API

        - `OmittedReasoningContent object { signature, type }`

          A placeholder for reasoning content we know is present, but isn't returned by the provider (e.g. OpenAI GPT-5 on ChatCompletions)

      - `string`

    - `role: "user" or "system" or "assistant"`

      The role of the participant.

      - `"user"`

      - `"system"`

      - `"assistant"`

    - `batch_item_id: optional string`

      The id of the LLMBatchItem that this message is associated with

    - `group_id: optional string`

      The multi-agent group that the message was sent in

    - `name: optional string`

      The name of the participant.

    - `otid: optional string`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `sender_id: optional string`

      The id of the sender of the message, can be an identity id or agent id

    - `type: optional "message"`

      The message type to be created.

      - `"message"`

  - `ApprovalCreate object { approval_request_id, approvals, approve, 4 more }`

    Input to approve or deny a tool call request

    - `approval_request_id: optional string`

      The message ID of the approval request

    - `approvals: optional array of ApprovalReturn or ToolReturn`

      The list of approval responses

      - `ApprovalReturn object { approve, tool_call_id, reason, type }`

        - `approve: boolean`

          Whether the tool has been approved

        - `tool_call_id: string`

          The ID of the tool call that corresponds to this approval

        - `reason: optional string`

          An optional explanation for the provided approval status

        - `type: optional "approval"`

          The message type to be created.

          - `"approval"`

      - `ToolReturn object { status, tool_call_id, tool_return, 3 more }`

        - `status: "success" or "error"`

          - `"success"`

          - `"error"`

        - `tool_call_id: string`

        - `tool_return: array of TextContent or ImageContent or string`

          The tool return value - either a string or list of content parts (text/image)

          - `array of TextContent or ImageContent`

            - `TextContent object { text, signature, type }`

            - `ImageContent object { source, type }`

          - `string`

        - `stderr: optional array of string`

        - `stdout: optional array of string`

        - `type: optional "tool"`

          The message type to be created.

          - `"tool"`

    - `approve: optional boolean`

      Whether the tool has been approved

    - `group_id: optional string`

      The multi-agent group that the message was sent in

    - `otid: optional string`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `reason: optional string`

      An optional explanation for the provided approval status

    - `type: optional "approval"`

      The message type to be created.

      - `"approval"`

  - `ToolReturnCreate object { tool_returns, group_id, otid, type }`

    Submit tool return(s) from client-side tool execution.

    This is the preferred way to send tool results back to the agent after
    client-side tool execution. It is equivalent to sending an ApprovalCreate
    with tool return approvals, but provides a cleaner API for the common case.

    - `tool_returns: array of ToolReturn`

      List of tool returns from client-side execution

      - `status: "success" or "error"`

      - `tool_call_id: string`

      - `tool_return: array of TextContent or ImageContent or string`

        The tool return value - either a string or list of content parts (text/image)

      - `stderr: optional array of string`

      - `stdout: optional array of string`

      - `type: optional "tool"`

        The message type to be created.

    - `group_id: optional string`

      The multi-agent group that the message was sent in

    - `otid: optional string`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `type: optional "tool_return"`

      The message type to be created.

      - `"tool_return"`

- `override_model: optional string`

  Model handle to use for this request instead of the agent's default model. This allows sending a message to a different model without changing the agent's configuration.

- `override_system: optional string`

  Optional per-request system prompt override. When set, this is passed directly to the underlying LLM request and bypasses the persisted/compiled system message for that request.

- `return_logprobs: optional boolean`

  If True, returns log probabilities of the output tokens in the response. Useful for RL training. Only supported for OpenAI-compatible providers (including SGLang).

- `return_token_ids: optional boolean`

  If True, returns token IDs and logprobs for ALL LLM generations in the agent step, not just the last one. Uses SGLang native /generate endpoint. Returns 'turns' field with TurnTokenData for each assistant/tool turn. Required for proper multi-turn RL training with loss masking.

- `stream_tokens: optional boolean`

  Flag to determine if individual tokens should be streamed, rather than streaming per step (only used when streaming=true).

- `streaming: optional boolean`

  If True (default), returns a streaming response (Server-Sent Events). If False, returns a complete JSON response.

- `top_logprobs: optional number`

  Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

- `use_assistant_message: optional boolean`

  Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

### Returns

- `LettaResponse object { messages, stop_reason, usage, 2 more }`

  Response object from an agent interaction, consisting of the new messages generated by the agent and usage statistics.
  The type of the returned messages can be either `Message` or `LettaMessage`, depending on what was specified in the request.

  Attributes:
  messages (List[Union[Message, LettaMessage]]): The messages returned by the agent.
  usage (LettaUsageStatistics): The usage statistics

  - `messages: array of Message`

    The messages returned by the agent.

    - `SystemMessage object { id, content, date, 8 more }`

      A message generated by the system. Never streamed back on a response, only used for cursor pagination.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      content (str): The message content sent by the system

      - `id: string`

      - `content: string`

        The message content sent by the system

      - `date: string`

      - `is_err: optional boolean`

      - `message_type: optional "system_message"`

        The type of the message.

        - `"system_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

    - `UserMessage object { id, content, date, 8 more }`

      A message sent by the user. Never streamed back on a response, only used for cursor pagination.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      content (Union[str, List[LettaUserMessageContentUnion]]): The message content sent by the user (can be a string or an array of multi-modal content parts)

      - `id: string`

      - `content: array of LettaUserMessageContentUnion or string`

        The message content sent by the user (can be a string or an array of multi-modal content parts)

        - `array of LettaUserMessageContentUnion`

          - `TextContent object { text, signature, type }`

            - `text: string`

              The text content of the message.

            - `signature: optional string`

              Stores a unique identifier for any reasoning associated with this text content.

            - `type: optional "text"`

              The type of the message.

              - `"text"`

          - `ImageContent object { source, type }`

            - `source: object { url, type }  or object { data, media_type, detail, type }  or object { file_id, data, detail, 2 more }`

              The source of the image.

              - `URL object { url, type }`

                - `url: string`

                  The URL of the image.

                - `type: optional "url"`

                  The source type for the image.

                  - `"url"`

              - `Base64 object { data, media_type, detail, type }`

                - `data: string`

                  The base64 encoded image data.

                - `media_type: string`

                  The media type for the image.

                - `detail: optional string`

                  What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

                - `type: optional "base64"`

                  The source type for the image.

                  - `"base64"`

              - `Letta object { file_id, data, detail, 2 more }`

                - `file_id: string`

                  The unique identifier of the image file persisted in storage.

                - `data: optional string`

                  The base64 encoded image data.

                - `detail: optional string`

                  What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

                - `media_type: optional string`

                  The media type for the image.

                - `type: optional "letta"`

                  The source type for the image.

                  - `"letta"`

            - `type: optional "image"`

              The type of the message.

              - `"image"`

        - `string`

      - `date: string`

      - `is_err: optional boolean`

      - `message_type: optional "user_message"`

        The type of the message.

        - `"user_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

    - `ReasoningMessage object { id, date, reasoning, 10 more }`

      Representation of an agent's internal reasoning.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      source (Literal["reasoner_model", "non_reasoner_model"]): Whether the reasoning
      content was generated natively by a reasoner model or derived via prompting
      reasoning (str): The internal reasoning of the agent
      signature (Optional[str]): The model-generated signature of the reasoning step

      - `id: string`

      - `date: string`

      - `reasoning: string`

      - `is_err: optional boolean`

      - `message_type: optional "reasoning_message"`

        The type of the message.

        - `"reasoning_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `signature: optional string`

      - `source: optional "reasoner_model" or "non_reasoner_model"`

        - `"reasoner_model"`

        - `"non_reasoner_model"`

      - `step_id: optional string`

    - `HiddenReasoningMessage object { id, date, state, 9 more }`

      Representation of an agent's internal reasoning where reasoning content
      has been hidden from the response.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      state (Literal["redacted", "omitted"]): Whether the reasoning
      content was redacted by the provider or simply omitted by the API
      hidden_reasoning (Optional[str]): The internal reasoning of the agent

      - `id: string`

      - `date: string`

      - `state: "redacted" or "omitted"`

        - `"redacted"`

        - `"omitted"`

      - `hidden_reasoning: optional string`

      - `is_err: optional boolean`

      - `message_type: optional "hidden_reasoning_message"`

        The type of the message.

        - `"hidden_reasoning_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

    - `ToolCallMessage object { id, date, tool_call, 9 more }`

      A message representing a request to call a tool (generated by the LLM to trigger tool execution).

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      tool_call (Union[ToolCall, ToolCallDelta]): The tool call

      - `id: string`

      - `date: string`

      - `tool_call: ToolCall or ToolCallDelta`

        - `ToolCall object { arguments, name, tool_call_id }`

          - `arguments: string`

          - `name: string`

          - `tool_call_id: string`

        - `ToolCallDelta object { arguments, name, tool_call_id }`

          - `arguments: optional string`

          - `name: optional string`

          - `tool_call_id: optional string`

      - `is_err: optional boolean`

      - `message_type: optional "tool_call_message"`

        The type of the message.

        - `"tool_call_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

      - `tool_calls: optional array of ToolCall or ToolCallDelta`

        - `array of ToolCall`

          - `arguments: string`

          - `name: string`

          - `tool_call_id: string`

        - `ToolCallDelta object { arguments, name, tool_call_id }`

    - `ToolReturnMessage object { id, date, status, 13 more }`

      A message representing the return value of a tool call (generated by Letta executing the requested tool).

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      tool_return (str): The return value of the tool (deprecated, use tool_returns)
      status (Literal["success", "error"]): The status of the tool call (deprecated, use tool_returns)
      tool_call_id (str): A unique identifier for the tool call that generated this message (deprecated, use tool_returns)
      stdout (Optional[List(str)]): Captured stdout (e.g. prints, logs) from the tool invocation (deprecated, use tool_returns)
      stderr (Optional[List(str)]): Captured stderr from the tool invocation (deprecated, use tool_returns)
      tool_returns (Optional[List[ToolReturn]]): List of tool returns for multi-tool support

      - `id: string`

      - `date: string`

      - `status: "success" or "error"`

        - `"success"`

        - `"error"`

      - `tool_call_id: string`

      - `tool_return: string`

      - `is_err: optional boolean`

      - `message_type: optional "tool_return_message"`

        The type of the message.

        - `"tool_return_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `stderr: optional array of string`

      - `stdout: optional array of string`

      - `step_id: optional string`

      - `tool_returns: optional array of ToolReturn`

        - `status: "success" or "error"`

          - `"success"`

          - `"error"`

        - `tool_call_id: string`

        - `tool_return: array of TextContent or ImageContent or string`

          The tool return value - either a string or list of content parts (text/image)

          - `array of TextContent or ImageContent`

            - `TextContent object { text, signature, type }`

            - `ImageContent object { source, type }`

          - `string`

        - `stderr: optional array of string`

        - `stdout: optional array of string`

        - `type: optional "tool"`

          The message type to be created.

          - `"tool"`

    - `AssistantMessage object { id, content, date, 8 more }`

      A message sent by the LLM in response to user input. Used in the LLM context.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      content (Union[str, List[LettaAssistantMessageContentUnion]]): The message content sent by the agent (can be a string or an array of content parts)

      - `id: string`

      - `content: array of LettaAssistantMessageContentUnion or string`

        The message content sent by the agent (can be a string or an array of content parts)

        - `array of LettaAssistantMessageContentUnion`

          - `text: string`

            The text content of the message.

          - `signature: optional string`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type: optional "text"`

            The type of the message.

            - `"text"`

        - `string`

      - `date: string`

      - `is_err: optional boolean`

      - `message_type: optional "assistant_message"`

        The type of the message.

        - `"assistant_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

    - `ApprovalRequestMessage object { id, date, tool_call, 9 more }`

      A message representing a request for approval to call a tool (generated by the LLM to trigger tool execution).

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      tool_call (ToolCall): The tool call

      - `id: string`

      - `date: string`

      - `tool_call: ToolCall or ToolCallDelta`

        The tool call that has been requested by the llm to run

        - `ToolCall object { arguments, name, tool_call_id }`

        - `ToolCallDelta object { arguments, name, tool_call_id }`

      - `is_err: optional boolean`

      - `message_type: optional "approval_request_message"`

        The type of the message.

        - `"approval_request_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

      - `tool_calls: optional array of ToolCall or ToolCallDelta`

        The tool calls that have been requested by the llm to run, which are pending approval

        - `array of ToolCall`

          - `arguments: string`

          - `name: string`

          - `tool_call_id: string`

        - `ToolCallDelta object { arguments, name, tool_call_id }`

    - `ApprovalResponseMessage object { id, date, approval_request_id, 11 more }`

      A message representing a response form the user indicating whether a tool has been approved to run.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      approve: (bool) Whether the tool has been approved
      approval_request_id: The ID of the approval request
      reason: (Optional[str]) An optional explanation for the provided approval status

      - `id: string`

      - `date: string`

      - `approval_request_id: optional string`

        The message ID of the approval request

      - `approvals: optional array of ApprovalReturn or ToolReturn`

        The list of approval responses

        - `ApprovalReturn object { approve, tool_call_id, reason, type }`

          - `approve: boolean`

            Whether the tool has been approved

          - `tool_call_id: string`

            The ID of the tool call that corresponds to this approval

          - `reason: optional string`

            An optional explanation for the provided approval status

          - `type: optional "approval"`

            The message type to be created.

            - `"approval"`

        - `ToolReturn object { status, tool_call_id, tool_return, 3 more }`

          - `status: "success" or "error"`

          - `tool_call_id: string`

          - `tool_return: array of TextContent or ImageContent or string`

            The tool return value - either a string or list of content parts (text/image)

          - `stderr: optional array of string`

          - `stdout: optional array of string`

          - `type: optional "tool"`

            The message type to be created.

      - `approve: optional boolean`

        Whether the tool has been approved

      - `is_err: optional boolean`

      - `message_type: optional "approval_response_message"`

        The type of the message.

        - `"approval_response_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `reason: optional string`

        An optional explanation for the provided approval status

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

    - `SummaryMessage object { id, date, summary, 9 more }`

      A message representing a summary of the conversation. Sent to the LLM as a user or system message depending on the provider.

      - `id: string`

      - `date: string`

      - `summary: string`

      - `compaction_stats: optional object { context_window, messages_count_after, messages_count_before, 3 more }`

        Statistics about a memory compaction operation.

        - `context_window: number`

          The model's context window size

        - `messages_count_after: number`

          Number of messages after compaction

        - `messages_count_before: number`

          Number of messages before compaction

        - `trigger: string`

          What triggered the compaction (e.g., 'context_window_exceeded', 'post_step_context_check')

        - `context_tokens_after: optional number`

          Token count after compaction (message tokens only, does not include tool definitions)

        - `context_tokens_before: optional number`

          Token count before compaction (from LLM usage stats, includes full context sent to LLM)

      - `is_err: optional boolean`

      - `message_type: optional "summary_message"`

        - `"summary_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

    - `EventMessage object { id, date, event_data, 9 more }`

      A message for notifying the developer that an event that has occured (e.g. a compaction). Events are NOT part of the context window.

      - `id: string`

      - `date: string`

      - `event_data: map[unknown]`

      - `event_type: "compaction"`

        - `"compaction"`

      - `is_err: optional boolean`

      - `message_type: optional "event_message"`

        - `"event_message"`

      - `name: optional string`

      - `otid: optional string`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id: optional string`

      - `sender_id: optional string`

      - `seq_id: optional number`

      - `step_id: optional string`

  - `stop_reason: object { stop_reason, message_type }`

    The stop reason from Letta indicating why agent loop stopped execution.

    - `stop_reason: StopReasonType`

      The reason why execution stopped.

      - `"end_turn"`

      - `"error"`

      - `"llm_api_error"`

      - `"invalid_llm_response"`

      - `"invalid_tool_call"`

      - `"max_steps"`

      - `"max_tokens_exceeded"`

      - `"no_tool_call"`

      - `"tool_rule"`

      - `"cancelled"`

      - `"insufficient_credits"`

      - `"requires_approval"`

      - `"context_window_overflow_in_system_prompt"`

    - `message_type: optional "stop_reason"`

      The type of the message.

      - `"stop_reason"`

  - `usage: object { cache_write_tokens, cached_input_tokens, completion_tokens, 7 more }`

    The usage statistics of the agent.

    - `cache_write_tokens: optional number`

      The number of input tokens written to cache (Anthropic only). None if not reported by provider.

    - `cached_input_tokens: optional number`

      The number of input tokens served from cache. None if not reported by provider.

    - `completion_tokens: optional number`

      The number of tokens generated by the agent.

    - `context_tokens: optional number`

      Estimate of tokens currently in the context window.

    - `message_type: optional "usage_statistics"`

      - `"usage_statistics"`

    - `prompt_tokens: optional number`

      The number of tokens in the prompt.

    - `reasoning_tokens: optional number`

      The number of reasoning/thinking tokens generated. None if not reported by provider.

    - `run_ids: optional array of string`

      The background task run IDs associated with the agent interaction

    - `step_count: optional number`

      The number of steps taken by the agent.

    - `total_tokens: optional number`

      The total number of tokens processed by the agent.

  - `logprobs: optional object { content, refusal }`

    Log probabilities of the output tokens from the last LLM call. Only present if return_logprobs was enabled.

    - `content: optional array of object { token, logprob, top_logprobs, bytes }`

      - `token: string`

      - `logprob: number`

      - `top_logprobs: array of object { token, logprob, bytes }`

        - `token: string`

        - `logprob: number`

        - `bytes: optional array of number`

      - `bytes: optional array of number`

    - `refusal: optional array of object { token, logprob, top_logprobs, bytes }`

      - `token: string`

      - `logprob: number`

      - `top_logprobs: array of object { token, logprob, bytes }`

        - `token: string`

        - `logprob: number`

        - `bytes: optional array of number`

      - `bytes: optional array of number`

  - `turns: optional array of object { role, content, output_ids, 2 more }`

    Token data for all LLM generations in multi-turn agent interaction. Includes token IDs and logprobs for each assistant turn, plus tool result content. Only present if return_token_ids was enabled. Used for RL training with loss masking.

    - `role: "assistant" or "tool"`

      Role of this turn: 'assistant' for LLM generations (trainable), 'tool' for tool results (non-trainable).

      - `"assistant"`

      - `"tool"`

    - `content: optional string`

      Text content. For tool turns, client tokenizes this with loss_mask=0.

    - `output_ids: optional array of number`

      Token IDs from SGLang native endpoint. Only present for assistant turns.

    - `output_token_logprobs: optional array of array of unknown`

      Logprobs from SGLang: [[logprob, token_id, top_logprob_or_null], ...]. Only present for assistant turns.

    - `tool_name: optional string`

      Name of the tool called. Only present for tool turns.

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/messages \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
```

#### Response

```json
{
  "messages": [
    {
      "id": "id",
      "content": "content",
      "date": "2019-12-27T18:11:19.117Z",
      "is_err": true,
      "message_type": "system_message",
      "name": "name",
      "otid": "otid",
      "run_id": "run_id",
      "sender_id": "sender_id",
      "seq_id": 0,
      "step_id": "step_id"
    }
  ],
  "stop_reason": {
    "stop_reason": "end_turn",
    "message_type": "stop_reason"
  },
  "usage": {
    "cache_write_tokens": 0,
    "cached_input_tokens": 0,
    "completion_tokens": 0,
    "context_tokens": 0,
    "message_type": "usage_statistics",
    "prompt_tokens": 0,
    "reasoning_tokens": 0,
    "run_ids": [
      "string"
    ],
    "step_count": 0,
    "total_tokens": 0
  },
  "logprobs": {
    "content": [
      {
        "token": "token",
        "logprob": 0,
        "top_logprobs": [
          {
            "token": "token",
            "logprob": 0,
            "bytes": [
              0
            ]
          }
        ],
        "bytes": [
          0
        ]
      }
    ],
    "refusal": [
      {
        "token": "token",
        "logprob": 0,
        "top_logprobs": [
          {
            "token": "token",
            "logprob": 0,
            "bytes": [
              0
            ]
          }
        ],
        "bytes": [
          0
        ]
      }
    ]
  },
  "turns": [
    {
      "role": "assistant",
      "content": "content",
      "output_ids": [
        0
      ],
      "output_token_logprobs": [
        [
          {}
        ]
      ],
      "tool_name": "tool_name"
    }
  ]
}
```

## Retrieve Conversation Stream

**post** `/v1/conversations/{conversation_id}/stream`

Resume the stream for the most recent active run in a conversation.

This endpoint allows you to reconnect to an active background stream
for a conversation, enabling recovery from network interruptions.

**Agent-direct mode**: Pass conversation_id="default" with agent_id in request body
to retrieve the stream for the agent's most recent active run.

**Direct run access**: Pass run_id directly to skip run lookup entirely.
Useful for recovery from duplicate request 409 errors.

**OTID lookup**: Pass otid to look up the run_id from Redis.
Useful when you have the otid from a 409 error response.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Body Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `batch_size: optional number`

  Number of entries to read per batch.

- `include_pings: optional boolean`

  Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

- `otid: optional string`

  Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

- `poll_interval: optional number`

  Seconds to wait between polls when no new data.

- `run_id: optional string`

  Run ID to stream directly, bypassing run lookup. Use for recovery from duplicate requests.

- `starting_after: optional number`

  Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/stream \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## Compact Conversation

**post** `/v1/conversations/{conversation_id}/compact`

Compact (summarize) a conversation's message history.

This endpoint summarizes the in-context messages for a specific conversation,
reducing the message count while preserving important context.

**Agent-direct mode**: Pass conversation_id="default" with agent_id in request body
to compact the agent's default conversation messages.

**Deprecated**: Passing an agent ID as conversation_id still works but will be removed.

### Path Parameters

- `conversation_id: string`

  The conversation identifier. Can be a conversation ID ('conv-<uuid4>'), 'default' for agent-direct mode (with agent_id parameter), or an agent ID ('agent-<uuid4>') for backwards compatibility (deprecated).

### Body Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `compaction_settings: optional object { clip_chars, mode, model, 4 more }`

  Configuration for conversation compaction / summarization.

  Per-model settings (temperature,
  max tokens, etc.) are derived from the default configuration for that handle.

  - `clip_chars: optional number`

    The maximum length of the summary in characters. If none, no clipping is performed.

  - `mode: optional "all" or "sliding_window" or "self_compact_all" or "self_compact_sliding_window"`

    The type of summarization technique use.

    - `"all"`

    - `"sliding_window"`

    - `"self_compact_all"`

    - `"self_compact_sliding_window"`

  - `model: optional string`

    Model handle to use for sliding_window/all summarization (format: provider/model-name). If None, uses lightweight provider-specific defaults.

  - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

    Optional model settings used to override defaults for the summarizer model.

    - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openai"`

        The type of the provider.

        - `"openai"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

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

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

      SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "sglang"`

        The type of the provider.

        - `"sglang"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

          The reasoning effort to use when generating text reasoning models

          - `"none"`

          - `"minimal"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `tool_call_parser: optional string`

        SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

    - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "anthropic"`

        The type of the provider.

        - `"anthropic"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_ai"`

        The type of the provider.

        - `"google_ai"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "google_vertex"`

        The type of the provider.

        - `"google_vertex"`

      - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response schema for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking_config: optional object { include_thoughts, thinking_budget }`

        The thinking configuration for the model.

        - `include_thoughts: optional boolean`

          Whether to include thoughts in the model's response.

        - `thinking_budget: optional number`

          The thinking budget for the model.

    - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Azure OpenAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "azure"`

        The type of the provider.

        - `"azure"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      xAI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "xai"`

        The type of the provider.

        - `"xai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Moonshot/Kimi model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot"`

        The type of the provider.

        - `"moonshot"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

    - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

      Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "zai"`

        The type of the provider.

        - `"zai"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { clear_thinking, type }`

        The thinking configuration for GLM-4.5+ models.

        - `clear_thinking: optional boolean`

          If False, preserved thinking is used (recommended for agents).

        - `type: optional "enabled" or "disabled"`

          Whether thinking is enabled or disabled.

          - `"enabled"`

          - `"disabled"`

    - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

      Kimi Code model configuration (Anthropic-compatible).

      - `effort: optional "low" or "medium" or "high" or 2 more`

        Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

        - `"low"`

        - `"medium"`

        - `"high"`

        - `"xhigh"`

        - `"max"`

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "moonshot_coding"`

        The type of the provider.

        - `"moonshot_coding"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `strict: optional boolean`

        Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

      - `temperature: optional number`

        The temperature of the model.

      - `thinking: optional object { budget_tokens, type }`

        The thinking configuration for the model.

        - `budget_tokens: optional number`

          The maximum number of tokens the model can use for extended thinking.

        - `type: optional "enabled" or "disabled"`

          The type of thinking to use.

          - `"enabled"`

          - `"disabled"`

      - `verbosity: optional "low" or "medium" or "high"`

        Soft control for how verbose model output should be, used for GPT-5 models.

        - `"low"`

        - `"medium"`

        - `"high"`

    - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Groq model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "groq"`

        The type of the provider.

        - `"groq"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Deepseek model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "deepseek"`

        The type of the provider.

        - `"deepseek"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      Together AI model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "together"`

        The type of the provider.

        - `"together"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      AWS Bedrock model configuration.

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "bedrock"`

        The type of the provider.

        - `"bedrock"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

      Baseten model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "baseten"`

        The type of the provider.

        - `"baseten"`

      - `temperature: optional number`

        The temperature of the model.

    - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      OpenRouter model configuration (OpenAI-compatible).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "openrouter"`

        The type of the provider.

        - `"openrouter"`

      - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

        The response format for the model.

        - `TextResponseFormat object { type }`

          Response format for plain text responses.

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

      - `temperature: optional number`

        The temperature of the model.

    - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

      ChatGPT OAuth model configuration (uses ChatGPT backend API).

      - `max_output_tokens: optional number`

        The maximum number of tokens the model can generate.

      - `parallel_tool_calls: optional boolean`

        Whether to enable parallel tool calling.

      - `provider_type: optional "chatgpt_oauth"`

        The type of the provider.

        - `"chatgpt_oauth"`

      - `reasoning: optional object { reasoning_effort }`

        The reasoning configuration for the model.

        - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

          The reasoning effort level for GPT-5.x and o-series models.

          - `"none"`

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

      - `temperature: optional number`

        The temperature of the model.

  - `prompt: optional string`

    The prompt to use for summarization. If None, uses mode-specific default.

  - `prompt_acknowledgement: optional boolean`

    Whether to include an acknowledgement post-prompt (helps prevent non-summary outputs).

  - `sliding_window_percentage: optional number`

    The percentage of the context window to keep post-summarization (only used in sliding window modes).

### Returns

- `CompactionResponse object { num_messages_after, num_messages_before, summary }`

  - `num_messages_after: number`

  - `num_messages_before: number`

  - `summary: string`

### Example

```http
curl https://api.letta.com/v1/conversations/$CONVERSATION_ID/compact \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "num_messages_after": 0,
  "num_messages_before": 0,
  "summary": "summary"
}
```

## Domain Types

### Compaction Request

- `CompactionRequest object { compaction_settings }`

  - `compaction_settings: optional object { clip_chars, mode, model, 4 more }`

    Configuration for conversation compaction / summarization.

    Per-model settings (temperature,
    max tokens, etc.) are derived from the default configuration for that handle.

    - `clip_chars: optional number`

      The maximum length of the summary in characters. If none, no clipping is performed.

    - `mode: optional "all" or "sliding_window" or "self_compact_all" or "self_compact_sliding_window"`

      The type of summarization technique use.

      - `"all"`

      - `"sliding_window"`

      - `"self_compact_all"`

      - `"self_compact_sliding_window"`

    - `model: optional string`

      Model handle to use for sliding_window/all summarization (format: provider/model-name). If None, uses lightweight provider-specific defaults.

    - `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

      Optional model settings used to override defaults for the summarizer model.

      - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "openai"`

          The type of the provider.

          - `"openai"`

        - `reasoning: optional object { reasoning_effort }`

          The reasoning configuration for the model.

          - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

            The reasoning effort to use when generating text reasoning models

            - `"none"`

            - `"minimal"`

            - `"low"`

            - `"medium"`

            - `"high"`

            - `"xhigh"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

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

        - `strict: optional boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature: optional number`

          The temperature of the model.

      - `Sglang object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }`

        SGLang model configuration (OpenAI-compatible runtime with SGLang-specific parsing).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "sglang"`

          The type of the provider.

          - `"sglang"`

        - `reasoning: optional object { reasoning_effort }`

          The reasoning configuration for the model.

          - `reasoning_effort: optional "none" or "minimal" or "low" or 3 more`

            The reasoning effort to use when generating text reasoning models

            - `"none"`

            - `"minimal"`

            - `"low"`

            - `"medium"`

            - `"high"`

            - `"xhigh"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `strict: optional boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature: optional number`

          The temperature of the model.

        - `tool_call_parser: optional string`

          SGLang tool call parser name (for example 'glm47', 'qwen25', or 'hermes').

      - `AnthropicModelSettings object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

        - `effort: optional "low" or "medium" or "high" or 2 more`

          Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

          - `"max"`

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "anthropic"`

          The type of the provider.

          - `"anthropic"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `strict: optional boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature: optional number`

          The temperature of the model.

        - `thinking: optional object { budget_tokens, type }`

          The thinking configuration for the model.

          - `budget_tokens: optional number`

            The maximum number of tokens the model can use for extended thinking.

          - `type: optional "enabled" or "disabled"`

            The type of thinking to use.

            - `"enabled"`

            - `"disabled"`

        - `verbosity: optional "low" or "medium" or "high"`

          Soft control for how verbose model output should be, used for GPT-5 models.

          - `"low"`

          - `"medium"`

          - `"high"`

      - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "google_ai"`

          The type of the provider.

          - `"google_ai"`

        - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response schema for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

        - `thinking_config: optional object { include_thoughts, thinking_budget }`

          The thinking configuration for the model.

          - `include_thoughts: optional boolean`

            Whether to include thoughts in the model's response.

          - `thinking_budget: optional number`

            The thinking budget for the model.

      - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "google_vertex"`

          The type of the provider.

          - `"google_vertex"`

        - `response_schema: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response schema for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

        - `thinking_config: optional object { include_thoughts, thinking_budget }`

          The thinking configuration for the model.

          - `include_thoughts: optional boolean`

            Whether to include thoughts in the model's response.

          - `thinking_budget: optional number`

            The thinking budget for the model.

      - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        Azure OpenAI model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "azure"`

          The type of the provider.

          - `"azure"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

      - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        xAI model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "xai"`

          The type of the provider.

          - `"xai"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

      - `Moonshot object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

        Moonshot/Kimi model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "moonshot"`

          The type of the provider.

          - `"moonshot"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `strict: optional boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature: optional number`

          The temperature of the model.

      - `Zai object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

        Z.ai (ZhipuAI) model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "zai"`

          The type of the provider.

          - `"zai"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

        - `thinking: optional object { clear_thinking, type }`

          The thinking configuration for GLM-4.5+ models.

          - `clear_thinking: optional boolean`

            If False, preserved thinking is used (recommended for agents).

          - `type: optional "enabled" or "disabled"`

            Whether thinking is enabled or disabled.

            - `"enabled"`

            - `"disabled"`

      - `MoonshotCoding object { effort, max_output_tokens, parallel_tool_calls, 6 more }`

        Kimi Code model configuration (Anthropic-compatible).

        - `effort: optional "low" or "medium" or "high" or 2 more`

          Effort level for supported Anthropic models (controls token spending). 'xhigh' and 'max' are available on Opus 4.6+. Not setting this gives similar performance to 'high'.

          - `"low"`

          - `"medium"`

          - `"high"`

          - `"xhigh"`

          - `"max"`

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "moonshot_coding"`

          The type of the provider.

          - `"moonshot_coding"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `strict: optional boolean`

          Enable strict mode for tool calling. When true, tool outputs are guaranteed to match JSON schemas.

        - `temperature: optional number`

          The temperature of the model.

        - `thinking: optional object { budget_tokens, type }`

          The thinking configuration for the model.

          - `budget_tokens: optional number`

            The maximum number of tokens the model can use for extended thinking.

          - `type: optional "enabled" or "disabled"`

            The type of thinking to use.

            - `"enabled"`

            - `"disabled"`

        - `verbosity: optional "low" or "medium" or "high"`

          Soft control for how verbose model output should be, used for GPT-5 models.

          - `"low"`

          - `"medium"`

          - `"high"`

      - `GroqModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        Groq model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "groq"`

          The type of the provider.

          - `"groq"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

      - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        Deepseek model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "deepseek"`

          The type of the provider.

          - `"deepseek"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

      - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        Together AI model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "together"`

          The type of the provider.

          - `"together"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

      - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        AWS Bedrock model configuration.

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "bedrock"`

          The type of the provider.

          - `"bedrock"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

      - `Baseten object { max_output_tokens, parallel_tool_calls, provider_type, temperature }`

        Baseten model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "baseten"`

          The type of the provider.

          - `"baseten"`

        - `temperature: optional number`

          The temperature of the model.

      - `Openrouter object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        OpenRouter model configuration (OpenAI-compatible).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "openrouter"`

          The type of the provider.

          - `"openrouter"`

        - `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

          The response format for the model.

          - `TextResponseFormat object { type }`

            Response format for plain text responses.

          - `JsonSchemaResponseFormat object { json_schema, type }`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat object { type }`

            Response format for JSON object responses.

        - `temperature: optional number`

          The temperature of the model.

      - `ChatgptOAuth object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

        ChatGPT OAuth model configuration (uses ChatGPT backend API).

        - `max_output_tokens: optional number`

          The maximum number of tokens the model can generate.

        - `parallel_tool_calls: optional boolean`

          Whether to enable parallel tool calling.

        - `provider_type: optional "chatgpt_oauth"`

          The type of the provider.

          - `"chatgpt_oauth"`

        - `reasoning: optional object { reasoning_effort }`

          The reasoning configuration for the model.

          - `reasoning_effort: optional "none" or "low" or "medium" or 2 more`

            The reasoning effort level for GPT-5.x and o-series models.

            - `"none"`

            - `"low"`

            - `"medium"`

            - `"high"`

            - `"xhigh"`

        - `temperature: optional number`

          The temperature of the model.

    - `prompt: optional string`

      The prompt to use for summarization. If None, uses mode-specific default.

    - `prompt_acknowledgement: optional boolean`

      Whether to include an acknowledgement post-prompt (helps prevent non-summary outputs).

    - `sliding_window_percentage: optional number`

      The percentage of the context window to keep post-summarization (only used in sliding window modes).

### Compaction Response

- `CompactionResponse object { num_messages_after, num_messages_before, summary }`

  - `num_messages_after: number`

  - `num_messages_before: number`

  - `summary: string`

### Message Stream Response

- `MessageStreamResponse = unknown`
