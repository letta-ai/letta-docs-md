# Agents

## List Agents For Block

**get** `/v1/blocks/{block_id}/agents`

Retrieves all agents associated with the specified block.
Raises a 404 if the block does not exist.

### Path Parameters

- `block_id: string`

  The ID of the block in the format 'block-<uuid4>'

### Query Parameters

- `after: optional string`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `before: optional string`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `include: optional array of "agent.blocks" or "agent.identities" or "agent.managed_group" or 5 more`

  Specify which relational fields to include in the response. No relationships are included by default.

  - `"agent.blocks"`

  - `"agent.identities"`

  - `"agent.managed_group"`

  - `"agent.pending_approval"`

  - `"agent.secrets"`

  - `"agent.sources"`

  - `"agent.tags"`

  - `"agent.tools"`

- `include_relationships: optional array of string`

  Specify which relational fields (e.g., 'tools', 'sources', 'memory') to include in the response. If not provided, all relationships are loaded by default. Using this can optimize performance by reducing unnecessary joins.This is a legacy parameter, and no longer supported after 1.0.0 SDK versions.

- `limit: optional number`

  Maximum number of agents to return

- `order: optional "asc" or "desc"`

  Sort order for agents by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

### Returns

- `id: string`

  The id of the agent. Assigned by the database.

- `agent_type: AgentType`

  The type of agent.

  - `"memgpt_agent"`

  - `"memgpt_v2_agent"`

  - `"letta_v1_agent"`

  - `"react_agent"`

  - `"workflow_agent"`

  - `"split_thread_agent"`

  - `"sleeptime_agent"`

  - `"voice_convo_agent"`

  - `"voice_sleeptime_agent"`

- `blocks: array of Block`

  The memory blocks used by the agent.

  - `value: string`

    Value of the block.

  - `id: optional string`

    The human-friendly ID of the Block

  - `base_template_id: optional string`

    The base template id of the block.

  - `created_by_id: optional string`

    The id of the user that made this Block.

  - `deployment_id: optional string`

    The id of the deployment.

  - `description: optional string`

    Description of the block.

  - `entity_id: optional string`

    The id of the entity within the template.

  - `hidden: optional boolean`

    If set to True, the block will be hidden.

  - `is_template: optional boolean`

    Whether the block is a template (e.g. saved human/persona options).

  - `label: optional string`

    Label of the block (e.g. 'human', 'persona') in the context window.

  - `last_updated_by_id: optional string`

    The id of the user that last updated this Block.

  - `limit: optional number`

    Character limit of the block.

  - `metadata: optional map[unknown]`

    Metadata of the block.

  - `preserve_on_migration: optional boolean`

    Preserve the block on template migration.

  - `project_id: optional string`

    The associated project id.

  - `read_only: optional boolean`

    Whether the agent has read-only access to the block.

  - `tags: optional array of string`

    The tags associated with the block.

  - `template_id: optional string`

    The id of the template.

  - `template_name: optional string`

    Name of the block if it is a template.

- `llm_config: LlmConfig`

  Deprecated: Use `model` field instead. The LLM configuration used by the agent.

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

- `memory: object { blocks, agent_type, file_blocks, 2 more }`

  Deprecated: Use `blocks` field instead. The in-context memory of the agent.

  - `blocks: array of Block`

    Memory blocks contained in the agent's in-context memory

    - `value: string`

      Value of the block.

    - `id: optional string`

      The human-friendly ID of the Block

    - `base_template_id: optional string`

      The base template id of the block.

    - `created_by_id: optional string`

      The id of the user that made this Block.

    - `deployment_id: optional string`

      The id of the deployment.

    - `description: optional string`

      Description of the block.

    - `entity_id: optional string`

      The id of the entity within the template.

    - `hidden: optional boolean`

      If set to True, the block will be hidden.

    - `is_template: optional boolean`

      Whether the block is a template (e.g. saved human/persona options).

    - `label: optional string`

      Label of the block (e.g. 'human', 'persona') in the context window.

    - `last_updated_by_id: optional string`

      The id of the user that last updated this Block.

    - `limit: optional number`

      Character limit of the block.

    - `metadata: optional map[unknown]`

      Metadata of the block.

    - `preserve_on_migration: optional boolean`

      Preserve the block on template migration.

    - `project_id: optional string`

      The associated project id.

    - `read_only: optional boolean`

      Whether the agent has read-only access to the block.

    - `tags: optional array of string`

      The tags associated with the block.

    - `template_id: optional string`

      The id of the template.

    - `template_name: optional string`

      Name of the block if it is a template.

  - `agent_type: optional AgentType or string`

    Agent type controlling prompt rendering.

    - `AgentType = "memgpt_agent" or "memgpt_v2_agent" or "letta_v1_agent" or 6 more`

      Enum to represent the type of agent.

    - `string`

  - `file_blocks: optional array of object { file_id, is_open, source_id, 20 more }`

    Special blocks representing the agent's in-context memory of an attached file

    - `file_id: string`

      Unique identifier of the file.

    - `is_open: boolean`

      True if the agent currently has the file open.

    - `source_id: string`

      Deprecated: Use `folder_id` field instead. Unique identifier of the source.

    - `value: string`

      Value of the block.

    - `id: optional string`

      The human-friendly ID of the Block

    - `base_template_id: optional string`

      The base template id of the block.

    - `created_by_id: optional string`

      The id of the user that made this Block.

    - `deployment_id: optional string`

      The id of the deployment.

    - `description: optional string`

      Description of the block.

    - `entity_id: optional string`

      The id of the entity within the template.

    - `hidden: optional boolean`

      If set to True, the block will be hidden.

    - `is_template: optional boolean`

      Whether the block is a template (e.g. saved human/persona options).

    - `label: optional string`

      Label of the block (e.g. 'human', 'persona') in the context window.

    - `last_accessed_at: optional string`

      UTC timestamp of the agent’s most recent access to this file. Any operations from the open, close, or search tools will update this field.

    - `last_updated_by_id: optional string`

      The id of the user that last updated this Block.

    - `limit: optional number`

      Character limit of the block.

    - `metadata: optional map[unknown]`

      Metadata of the block.

    - `preserve_on_migration: optional boolean`

      Preserve the block on template migration.

    - `project_id: optional string`

      The associated project id.

    - `read_only: optional boolean`

      Whether the agent has read-only access to the block.

    - `tags: optional array of string`

      The tags associated with the block.

    - `template_id: optional string`

      The id of the template.

    - `template_name: optional string`

      Name of the block if it is a template.

  - `git_enabled: optional boolean`

    Whether this agent uses git-backed memory with structured labels.

  - `prompt_template: optional string`

    Deprecated. Ignored for performance.

- `name: string`

  The name of the agent.

- `sources: array of object { id, embedding_config, name, 8 more }`

  Deprecated: Use `folders` field instead. The sources used by the agent.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the source.

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

  - `name: string`

    The name of the source.

  - `created_at: optional string`

    The timestamp when the source was created.

  - `created_by_id: optional string`

    The id of the user that made this Tool.

  - `description: optional string`

    The description of the source.

  - `instructions: optional string`

    Instructions for how to use the source.

  - `last_updated_by_id: optional string`

    The id of the user that made this Tool.

  - `metadata: optional map[unknown]`

    Metadata associated with the source.

  - `updated_at: optional string`

    The timestamp when the source was last updated.

  - `vector_db_provider: optional VectorDBProvider`

    The vector database provider used for this source's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

- `system: string`

  The system prompt used by the agent.

- `tags: array of string`

  The tags associated with the agent.

- `tools: array of Tool`

  The tools used by the agent.

  - `id: string`

    The human-friendly ID of the Tool

  - `args_json_schema: optional map[unknown]`

    The args JSON schema of the function.

  - `created_by_id: optional string`

    The id of the user that made this Tool.

  - `default_requires_approval: optional boolean`

    Default value for whether or not executing this tool requires approval.

  - `description: optional string`

    The description of the tool.

  - `enable_parallel_execution: optional boolean`

    If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

  - `json_schema: optional map[unknown]`

    The JSON schema of the function.

  - `last_updated_by_id: optional string`

    The id of the user that made this Tool.

  - `metadata_: optional map[unknown]`

    A dictionary of additional metadata for the tool.

  - `name: optional string`

    The name of the function.

  - `npm_requirements: optional array of NpmRequirement`

    Optional list of npm packages required by this tool.

    - `name: string`

      Name of the npm package.

    - `version: optional string`

      Optional version of the package, following semantic versioning.

  - `pip_requirements: optional array of PipRequirement`

    Optional list of pip packages required by this tool.

    - `name: string`

      Name of the pip package.

    - `version: optional string`

      Optional version of the package, following semantic versioning.

  - `project_id: optional string`

    The project id of the tool.

  - `return_char_limit: optional number`

    The maximum number of characters in the response.

  - `source_code: optional string`

    The source code of the function.

  - `source_type: optional string`

    The type of the source code.

  - `tags: optional array of string`

    Metadata tags.

  - `tool_type: optional ToolType`

    The type of the tool.

    - `"custom"`

    - `"letta_core"`

    - `"letta_memory_core"`

    - `"letta_multi_agent_core"`

    - `"letta_sleeptime_core"`

    - `"letta_voice_sleeptime_core"`

    - `"letta_builtin"`

    - `"letta_files_core"`

    - `"external_langchain"`

    - `"external_composio"`

    - `"external_mcp"`

- `base_template_id: optional string`

  The base template id of the agent.

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

        - `JsonSchemaResponseFormat object { json_schema, type }`

          Response format for JSON schema-based responses.

        - `JsonObjectResponseFormat object { type }`

          Response format for JSON object responses.

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

- `created_at: optional string`

  The timestamp when the object was created.

- `created_by_id: optional string`

  The id of the user that made this object.

- `deployment_id: optional string`

  The id of the deployment.

- `description: optional string`

  The description of the agent.

- `embedding: optional string`

  The embedding model handle used by the agent (format: provider/model-name).

- `embedding_config: optional EmbeddingConfig`

  Configuration for embedding model connection and processing parameters.

- `enable_sleeptime: optional boolean`

  If set to True, memory management will move to a background agent thread.

- `entity_id: optional string`

  The id of the entity within the template.

- `hidden: optional boolean`

  If set to True, the agent will be hidden.

- `identities: optional array of object { id, agent_ids, block_ids, 5 more }`

  The identities associated with this agent.

  - `id: string`

    The human-friendly ID of the Identity

  - `agent_ids: array of string`

    The IDs of the agents associated with the identity.

  - `block_ids: array of string`

    The IDs of the blocks associated with the identity.

  - `identifier_key: string`

    External, user-generated identifier key of the identity.

  - `identity_type: "org" or "user" or "other"`

    The type of the identity.

    - `"org"`

    - `"user"`

    - `"other"`

  - `name: string`

    The name of the identity.

  - `project_id: optional string`

    The project id of the identity, if applicable.

  - `properties: optional array of object { key, type, value }`

    List of properties associated with the identity

    - `key: string`

      The key of the property

    - `type: "string" or "number" or "boolean" or "json"`

      The type of the property

      - `"string"`

      - `"number"`

      - `"boolean"`

      - `"json"`

    - `value: string or number or boolean or map[unknown]`

      The value of the property

      - `string`

      - `number`

      - `boolean`

      - `map[unknown]`

- `identity_ids: optional array of string`

  Deprecated: Use `identities` field instead. The ids of the identities associated with this agent.

- `last_run_completion: optional string`

  The timestamp when the agent last completed a run.

- `last_run_duration_ms: optional number`

  The duration in milliseconds of the agent's last run.

- `last_stop_reason: optional StopReasonType`

  The stop reason from the agent's last run.

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

- `last_updated_by_id: optional string`

  The id of the user that made this object.

- `managed_group: optional object { id, agent_ids, description, 15 more }`

  The multi-agent group that this agent manages

  - `id: string`

    The id of the group. Assigned by the database.

  - `agent_ids: array of string`

  - `description: string`

  - `manager_type: "round_robin" or "supervisor" or "dynamic" or 3 more`

    - `"round_robin"`

    - `"supervisor"`

    - `"dynamic"`

    - `"sleeptime"`

    - `"voice_sleeptime"`

    - `"swarm"`

  - `base_template_id: optional string`

    The base template id.

  - `deployment_id: optional string`

    The id of the deployment.

  - `hidden: optional boolean`

    If set to True, the group will be hidden.

  - `last_processed_message_id: optional string`

  - `manager_agent_id: optional string`

  - `max_message_buffer_length: optional number`

    The desired maximum length of messages in the context window of the convo agent. This is a best effort, and may be off slightly due to user/assistant interleaving.

  - `max_turns: optional number`

  - `min_message_buffer_length: optional number`

    The desired minimum length of messages in the context window of the convo agent. This is a best effort, and may be off-by-one due to user/assistant interleaving.

  - `project_id: optional string`

    The associated project id.

  - `shared_block_ids: optional array of string`

  - `sleeptime_agent_frequency: optional number`

  - `template_id: optional string`

    The id of the template.

  - `termination_token: optional string`

  - `turns_counter: optional number`

- `max_files_open: optional number`

  Maximum number of files that can be open at once for this agent. Setting this too high may exceed the context window, which will break the agent.

- `message_buffer_autoclear: optional boolean`

  If set to True, the agent will not remember previous messages (though the agent will still retain state via core memory blocks and archival/recall memory). Not recommended unless you have an advanced use case.

- `message_ids: optional array of string`

  The ids of the messages in the agent's in-context memory.

- `metadata: optional map[unknown]`

  The metadata of the agent.

- `model: optional string`

  The model handle used by the agent (format: provider/model-name).

- `model_settings: optional OpenAIModelSettings or object { max_output_tokens, parallel_tool_calls, provider_type, 5 more }  or AnthropicModelSettings or 14 more`

  The model settings used by the agent.

  - `OpenAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 4 more }`

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

  - `GoogleAIModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

  - `GoogleVertexModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 3 more }`

  - `AzureModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Azure OpenAI model configuration (OpenAI-compatible).

  - `XaiModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    xAI model configuration (OpenAI-compatible).

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

  - `DeepseekModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Deepseek model configuration (OpenAI-compatible).

  - `TogetherModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    Together AI model configuration (OpenAI-compatible).

  - `BedrockModelSettings object { max_output_tokens, parallel_tool_calls, provider_type, 2 more }`

    AWS Bedrock model configuration.

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

- `multi_agent_group: optional object { id, agent_ids, description, 15 more }`

  Deprecated: Use `managed_group` field instead. The multi-agent group that this agent manages.

  - `id: string`

    The id of the group. Assigned by the database.

  - `agent_ids: array of string`

  - `description: string`

  - `manager_type: "round_robin" or "supervisor" or "dynamic" or 3 more`

    - `"round_robin"`

    - `"supervisor"`

    - `"dynamic"`

    - `"sleeptime"`

    - `"voice_sleeptime"`

    - `"swarm"`

  - `base_template_id: optional string`

    The base template id.

  - `deployment_id: optional string`

    The id of the deployment.

  - `hidden: optional boolean`

    If set to True, the group will be hidden.

  - `last_processed_message_id: optional string`

  - `manager_agent_id: optional string`

  - `max_message_buffer_length: optional number`

    The desired maximum length of messages in the context window of the convo agent. This is a best effort, and may be off slightly due to user/assistant interleaving.

  - `max_turns: optional number`

  - `min_message_buffer_length: optional number`

    The desired minimum length of messages in the context window of the convo agent. This is a best effort, and may be off-by-one due to user/assistant interleaving.

  - `project_id: optional string`

    The associated project id.

  - `shared_block_ids: optional array of string`

  - `sleeptime_agent_frequency: optional number`

  - `template_id: optional string`

    The id of the template.

  - `termination_token: optional string`

  - `turns_counter: optional number`

- `pending_approval: optional ApprovalRequestMessage`

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

      - `arguments: string`

      - `name: string`

      - `tool_call_id: string`

    - `ToolCallDelta object { arguments, name, tool_call_id }`

      - `arguments: optional string`

      - `name: optional string`

      - `tool_call_id: optional string`

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

- `per_file_view_window_char_limit: optional number`

  The per-file view window character limit for this agent. Setting this too high may exceed the context window, which will break the agent.

- `project_id: optional string`

  The id of the project the agent belongs to.

- `response_format: optional TextResponseFormat or JsonSchemaResponseFormat or JsonObjectResponseFormat`

  The response format used by the agent

  - `TextResponseFormat object { type }`

    Response format for plain text responses.

  - `JsonSchemaResponseFormat object { json_schema, type }`

    Response format for JSON schema-based responses.

  - `JsonObjectResponseFormat object { type }`

    Response format for JSON object responses.

- `secrets: optional array of AgentEnvironmentVariable`

  The environment variables for tool execution specific to this agent.

  - `agent_id: string`

    The ID of the agent this environment variable belongs to.

  - `key: string`

    The name of the environment variable.

  - `value: string`

    The value of the environment variable.

  - `id: optional string`

    The human-friendly ID of the Agent-env

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    An optional description of the environment variable.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

  - `value_enc: optional string`

    Encrypted secret value (stored as encrypted string)

- `template_id: optional string`

  The id of the template the agent belongs to.

- `timezone: optional string`

  The timezone of the agent (IANA format).

- `tool_exec_environment_variables: optional array of AgentEnvironmentVariable`

  Deprecated: use `secrets` field instead.

  - `agent_id: string`

    The ID of the agent this environment variable belongs to.

  - `key: string`

    The name of the environment variable.

  - `value: string`

    The value of the environment variable.

  - `id: optional string`

    The human-friendly ID of the Agent-env

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `description: optional string`

    An optional description of the environment variable.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `updated_at: optional string`

    The timestamp when the object was last updated.

  - `value_enc: optional string`

    Encrypted secret value (stored as encrypted string)

- `tool_rules: optional array of ChildToolRule or InitToolRule or TerminalToolRule or 6 more`

  The list of tool rules.

  - `ChildToolRule object { children, tool_name, child_arg_nodes, 2 more }`

    A ToolRule represents a tool that can be invoked by the agent.

    - `children: array of string`

      The children tools that can be invoked.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `child_arg_nodes: optional array of object { name, args }`

      Optional list of typed child argument overrides. Each node must reference a child in 'children'.

      - `name: string`

        The name of the child tool to invoke next.

      - `args: optional map[unknown]`

        Optional prefilled arguments for this child tool. Keys must match the tool's parameter names and values must satisfy the tool's JSON schema. Supports partial prefill; non-overlapping parameters are left to the model.

    - `prompt_template: optional string`

      Optional template string (ignored).

    - `type: optional "constrain_child_tools"`

      - `"constrain_child_tools"`

  - `InitToolRule object { tool_name, args, prompt_template, type }`

    Represents the initial tool rule configuration.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `args: optional map[unknown]`

      Optional prefilled arguments for this tool. When present, these values will override any LLM-provided arguments with the same keys during invocation. Keys must match the tool's parameter names and values must satisfy the tool's JSON schema. Supports partial prefill; non-overlapping parameters are left to the model.

    - `prompt_template: optional string`

      Optional template string (ignored). Rendering uses fast built-in formatting for performance.

    - `type: optional "run_first"`

      - `"run_first"`

  - `TerminalToolRule object { tool_name, prompt_template, type }`

    Represents a terminal tool rule configuration where if this tool gets called, it must end the agent loop.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `prompt_template: optional string`

      Optional template string (ignored).

    - `type: optional "exit_loop"`

      - `"exit_loop"`

  - `ConditionalToolRule object { child_output_mapping, tool_name, default_child, 3 more }`

    A ToolRule that conditionally maps to different child tools based on the output.

    - `child_output_mapping: map[string]`

      The output case to check for mapping

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `default_child: optional string`

      The default child tool to be called. If None, any tool can be called.

    - `prompt_template: optional string`

      Optional template string (ignored).

    - `require_output_mapping: optional boolean`

      Whether to throw an error when output doesn't match any case

    - `type: optional "conditional"`

      - `"conditional"`

  - `ContinueToolRule object { tool_name, prompt_template, type }`

    Represents a tool rule configuration where if this tool gets called, it must continue the agent loop.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `prompt_template: optional string`

      Optional template string (ignored).

    - `type: optional "continue_loop"`

      - `"continue_loop"`

  - `RequiredBeforeExitToolRule object { tool_name, prompt_template, type }`

    Represents a tool rule configuration where this tool must be called before the agent loop can exit.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `prompt_template: optional string`

      Optional template string (ignored).

    - `type: optional "required_before_exit"`

      - `"required_before_exit"`

  - `MaxCountPerStepToolRule object { max_count_limit, tool_name, prompt_template, type }`

    Represents a tool rule configuration which constrains the total number of times this tool can be invoked in a single step.

    - `max_count_limit: number`

      The max limit for the total number of times this tool can be invoked in a single step.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `prompt_template: optional string`

      Optional template string (ignored).

    - `type: optional "max_count_per_step"`

      - `"max_count_per_step"`

  - `ParentToolRule object { children, tool_name, prompt_template, type }`

    A ToolRule that only allows a child tool to be called if the parent has been called.

    - `children: array of string`

      The children tools that can be invoked.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `prompt_template: optional string`

      Optional template string (ignored).

    - `type: optional "parent_last_tool"`

      - `"parent_last_tool"`

  - `RequiresApprovalToolRule object { tool_name, prompt_template, type }`

    Represents a tool rule configuration which requires approval before the tool can be invoked.

    - `tool_name: string`

      The name of the tool. Must exist in the database for the user's organization.

    - `prompt_template: optional string`

      Optional template string (ignored). Rendering uses fast built-in formatting for performance.

    - `type: optional "requires_approval"`

      - `"requires_approval"`

- `updated_at: optional string`

  The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/blocks/$BLOCK_ID/agents \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  {
    "id": "id",
    "agent_type": "memgpt_agent",
    "blocks": [
      {
        "value": "value",
        "id": "block-123e4567-e89b-12d3-a456-426614174000",
        "base_template_id": "base_template_id",
        "created_by_id": "created_by_id",
        "deployment_id": "deployment_id",
        "description": "description",
        "entity_id": "entity_id",
        "hidden": true,
        "is_template": true,
        "label": "label",
        "last_updated_by_id": "last_updated_by_id",
        "limit": 0,
        "metadata": {
          "foo": "bar"
        },
        "preserve_on_migration": true,
        "project_id": "project_id",
        "read_only": true,
        "tags": [
          "string"
        ],
        "template_id": "template_id",
        "template_name": "template_name"
      }
    ],
    "llm_config": {
      "context_window": 0,
      "model": "model",
      "model_endpoint_type": "openai",
      "compatibility_type": "gguf",
      "display_name": "display_name",
      "effort": "low",
      "enable_reasoner": true,
      "frequency_penalty": 0,
      "handle": "handle",
      "max_reasoning_tokens": 0,
      "max_tokens": 0,
      "model_endpoint": "model_endpoint",
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
    },
    "memory": {
      "blocks": [
        {
          "value": "value",
          "id": "block-123e4567-e89b-12d3-a456-426614174000",
          "base_template_id": "base_template_id",
          "created_by_id": "created_by_id",
          "deployment_id": "deployment_id",
          "description": "description",
          "entity_id": "entity_id",
          "hidden": true,
          "is_template": true,
          "label": "label",
          "last_updated_by_id": "last_updated_by_id",
          "limit": 0,
          "metadata": {
            "foo": "bar"
          },
          "preserve_on_migration": true,
          "project_id": "project_id",
          "read_only": true,
          "tags": [
            "string"
          ],
          "template_id": "template_id",
          "template_name": "template_name"
        }
      ],
      "agent_type": "memgpt_agent",
      "file_blocks": [
        {
          "file_id": "file_id",
          "is_open": true,
          "source_id": "source_id",
          "value": "value",
          "id": "block-123e4567-e89b-12d3-a456-426614174000",
          "base_template_id": "base_template_id",
          "created_by_id": "created_by_id",
          "deployment_id": "deployment_id",
          "description": "description",
          "entity_id": "entity_id",
          "hidden": true,
          "is_template": true,
          "label": "label",
          "last_accessed_at": "2019-12-27T18:11:19.117Z",
          "last_updated_by_id": "last_updated_by_id",
          "limit": 0,
          "metadata": {
            "foo": "bar"
          },
          "preserve_on_migration": true,
          "project_id": "project_id",
          "read_only": true,
          "tags": [
            "string"
          ],
          "template_id": "template_id",
          "template_name": "template_name"
        }
      ],
      "git_enabled": true,
      "prompt_template": "prompt_template"
    },
    "name": "name",
    "sources": [
      {
        "id": "source-123e4567-e89b-12d3-a456-426614174000",
        "embedding_config": {
          "embedding_dim": 0,
          "embedding_endpoint_type": "openai",
          "embedding_model": "embedding_model",
          "azure_deployment": "azure_deployment",
          "azure_endpoint": "azure_endpoint",
          "azure_version": "azure_version",
          "batch_size": 0,
          "embedding_chunk_size": 0,
          "embedding_endpoint": "embedding_endpoint",
          "handle": "handle"
        },
        "name": "name",
        "created_at": "2019-12-27T18:11:19.117Z",
        "created_by_id": "created_by_id",
        "description": "description",
        "instructions": "instructions",
        "last_updated_by_id": "last_updated_by_id",
        "metadata": {
          "foo": "bar"
        },
        "updated_at": "2019-12-27T18:11:19.117Z",
        "vector_db_provider": "native"
      }
    ],
    "system": "system",
    "tags": [
      "string"
    ],
    "tools": [
      {
        "id": "tool-123e4567-e89b-12d3-a456-426614174000",
        "args_json_schema": {
          "foo": "bar"
        },
        "created_by_id": "created_by_id",
        "default_requires_approval": true,
        "description": "description",
        "enable_parallel_execution": true,
        "json_schema": {
          "foo": "bar"
        },
        "last_updated_by_id": "last_updated_by_id",
        "metadata_": {
          "foo": "bar"
        },
        "name": "name",
        "npm_requirements": [
          {
            "name": "x",
            "version": "version"
          }
        ],
        "pip_requirements": [
          {
            "name": "x",
            "version": "version"
          }
        ],
        "project_id": "project_id",
        "return_char_limit": 1,
        "source_code": "source_code",
        "source_type": "source_type",
        "tags": [
          "string"
        ],
        "tool_type": "custom"
      }
    ],
    "base_template_id": "base_template_id",
    "compaction_settings": {
      "clip_chars": 0,
      "mode": "all",
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
      "prompt": "prompt",
      "prompt_acknowledgement": true,
      "sliding_window_percentage": 0
    },
    "created_at": "2019-12-27T18:11:19.117Z",
    "created_by_id": "created_by_id",
    "deployment_id": "deployment_id",
    "description": "description",
    "embedding": "embedding",
    "embedding_config": {
      "embedding_dim": 0,
      "embedding_endpoint_type": "openai",
      "embedding_model": "embedding_model",
      "azure_deployment": "azure_deployment",
      "azure_endpoint": "azure_endpoint",
      "azure_version": "azure_version",
      "batch_size": 0,
      "embedding_chunk_size": 0,
      "embedding_endpoint": "embedding_endpoint",
      "handle": "handle"
    },
    "enable_sleeptime": true,
    "entity_id": "entity_id",
    "hidden": true,
    "identities": [
      {
        "id": "identity-123e4567-e89b-12d3-a456-426614174000",
        "agent_ids": [
          "string"
        ],
        "block_ids": [
          "string"
        ],
        "identifier_key": "identifier_key",
        "identity_type": "org",
        "name": "name",
        "project_id": "project_id",
        "properties": [
          {
            "key": "key",
            "type": "string",
            "value": "string"
          }
        ]
      }
    ],
    "identity_ids": [
      "string"
    ],
    "last_run_completion": "2019-12-27T18:11:19.117Z",
    "last_run_duration_ms": 0,
    "last_stop_reason": "end_turn",
    "last_updated_by_id": "last_updated_by_id",
    "managed_group": {
      "id": "id",
      "agent_ids": [
        "string"
      ],
      "description": "description",
      "manager_type": "round_robin",
      "base_template_id": "base_template_id",
      "deployment_id": "deployment_id",
      "hidden": true,
      "last_processed_message_id": "last_processed_message_id",
      "manager_agent_id": "manager_agent_id",
      "max_message_buffer_length": 0,
      "max_turns": 0,
      "min_message_buffer_length": 0,
      "project_id": "project_id",
      "shared_block_ids": [
        "string"
      ],
      "sleeptime_agent_frequency": 0,
      "template_id": "template_id",
      "termination_token": "termination_token",
      "turns_counter": 0
    },
    "max_files_open": 0,
    "message_buffer_autoclear": true,
    "message_ids": [
      "string"
    ],
    "metadata": {
      "foo": "bar"
    },
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
    "multi_agent_group": {
      "id": "id",
      "agent_ids": [
        "string"
      ],
      "description": "description",
      "manager_type": "round_robin",
      "base_template_id": "base_template_id",
      "deployment_id": "deployment_id",
      "hidden": true,
      "last_processed_message_id": "last_processed_message_id",
      "manager_agent_id": "manager_agent_id",
      "max_message_buffer_length": 0,
      "max_turns": 0,
      "min_message_buffer_length": 0,
      "project_id": "project_id",
      "shared_block_ids": [
        "string"
      ],
      "sleeptime_agent_frequency": 0,
      "template_id": "template_id",
      "termination_token": "termination_token",
      "turns_counter": 0
    },
    "pending_approval": {
      "id": "id",
      "date": "2019-12-27T18:11:19.117Z",
      "tool_call": {
        "arguments": "arguments",
        "name": "name",
        "tool_call_id": "tool_call_id"
      },
      "is_err": true,
      "message_type": "approval_request_message",
      "name": "name",
      "otid": "otid",
      "run_id": "run_id",
      "sender_id": "sender_id",
      "seq_id": 0,
      "step_id": "step_id",
      "tool_calls": [
        {
          "arguments": "arguments",
          "name": "name",
          "tool_call_id": "tool_call_id"
        }
      ]
    },
    "per_file_view_window_char_limit": 0,
    "project_id": "project_id",
    "response_format": {
      "type": "text"
    },
    "secrets": [
      {
        "agent_id": "agent_id",
        "key": "key",
        "value": "value",
        "id": "agent-env-123e4567-e89b-12d3-a456-426614174000",
        "created_at": "2019-12-27T18:11:19.117Z",
        "created_by_id": "created_by_id",
        "description": "description",
        "last_updated_by_id": "last_updated_by_id",
        "updated_at": "2019-12-27T18:11:19.117Z",
        "value_enc": "value_enc"
      }
    ],
    "template_id": "template_id",
    "timezone": "timezone",
    "tool_exec_environment_variables": [
      {
        "agent_id": "agent_id",
        "key": "key",
        "value": "value",
        "id": "agent-env-123e4567-e89b-12d3-a456-426614174000",
        "created_at": "2019-12-27T18:11:19.117Z",
        "created_by_id": "created_by_id",
        "description": "description",
        "last_updated_by_id": "last_updated_by_id",
        "updated_at": "2019-12-27T18:11:19.117Z",
        "value_enc": "value_enc"
      }
    ],
    "tool_rules": [
      {
        "children": [
          "string"
        ],
        "tool_name": "tool_name",
        "child_arg_nodes": [
          {
            "name": "name",
            "args": {
              "foo": "bar"
            }
          }
        ],
        "prompt_template": "prompt_template",
        "type": "constrain_child_tools"
      }
    ],
    "updated_at": "2019-12-27T18:11:19.117Z"
  }
]
```
