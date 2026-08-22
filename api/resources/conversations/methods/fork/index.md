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
