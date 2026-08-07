## Detach Block From Agent

`client.agents.blocks.detach(stringblockID, BlockDetachParamsparams, RequestOptionsoptions?): AgentState`

**patch** `/v1/agents/{agent_id}/core-memory/blocks/detach/{block_id}`

Detach a core memory block from an agent.

### Parameters

- `blockID: string`

  The ID of the block in the format 'block-<uuid4>'

- `params: BlockDetachParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `AgentState`

  Representation of an agent's state. This is the state of the agent at a given time, and is persisted in the DB backend. The state has all the information needed to recreate a persisted agent.

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

  - `blocks: Array<Block>`

    The memory blocks used by the agent.

    - `value: string`

      Value of the block.

    - `id?: string`

      The human-friendly ID of the Block

    - `base_template_id?: string | null`

      The base template id of the block.

    - `created_by_id?: string | null`

      The id of the user that made this Block.

    - `deployment_id?: string | null`

      The id of the deployment.

    - `description?: string | null`

      Description of the block.

    - `entity_id?: string | null`

      The id of the entity within the template.

    - `hidden?: boolean | null`

      If set to True, the block will be hidden.

    - `is_template?: boolean`

      Whether the block is a template (e.g. saved human/persona options).

    - `label?: string | null`

      Label of the block (e.g. 'human', 'persona') in the context window.

    - `last_updated_by_id?: string | null`

      The id of the user that last updated this Block.

    - `limit?: number`

      Character limit of the block.

    - `metadata?: Record<string, unknown> | null`

      Metadata of the block.

    - `preserve_on_migration?: boolean | null`

      Preserve the block on template migration.

    - `project_id?: string | null`

      The associated project id.

    - `read_only?: boolean`

      Whether the agent has read-only access to the block.

    - `tags?: Array<string> | null`

      The tags associated with the block.

    - `template_id?: string | null`

      The id of the template.

    - `template_name?: string | null`

      Name of the block if it is a template.

  - `llm_config: LlmConfig`

    Deprecated: Use `model` field instead. The LLM configuration used by the agent.

    - `context_window: number`

      The context window size for the model.

    - `model: string`

      LLM model name.

    - `model_endpoint_type: "openai" | "anthropic" | "google_ai" | 27 more`

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

    - `compatibility_type?: "gguf" | "mlx" | null`

      The framework compatibility type for the model.

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

      Whether or not the model should use extended thinking if it is a 'reasoning' style model

    - `frequency_penalty?: number | null`

      Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim. From OpenAI: Number between -2.0 and 2.0.

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

    - `max_reasoning_tokens?: number`

      Configurable thinking budget for extended thinking. Used for enable_reasoner and also for Google Vertex models like Gemini 2.5 Flash. Minimum value is 1024 when used with enable_reasoner.

    - `max_tokens?: number | null`

      The maximum number of tokens to generate. If not set, the model will use its default value.

    - `model_endpoint?: string | null`

      The endpoint for the model.

    - `model_wrapper?: string | null`

      The wrapper for the model.

    - `parallel_tool_calls?: boolean | null`

      Deprecated: Use model_settings to configure parallel tool calls instead. If set to True, enables parallel tool calling. Defaults to False.

    - `provider_category?: ProviderCategory | null`

      The provider category for the model.

      - `"base"`

      - `"byok"`

    - `provider_name?: string | null`

      The provider name for the model.

    - `put_inner_thoughts_in_kwargs?: boolean | null`

      Puts 'inner_thoughts' as a kwarg in the function call if this is set to True. This helps with function calling performance and also the generation of inner thoughts.

    - `reasoning_effort?: "none" | "minimal" | "low" | 3 more | null`

      The reasoning effort to use when generating text reasoning models

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

      The temperature to use when generating text with the model. A higher temperature will result in more random text.

    - `tier?: string | null`

      The cost tier for the model (cloud only).

    - `tool_call_parser?: string | null`

      SGLang tool call parser name (e.g. 'glm47', 'qwen25', 'hermes'). Used by the SGLang native adapter to parse tool calls from raw model output.

    - `top_logprobs?: number | null`

      Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

    - `verbosity?: "low" | "medium" | "high" | null`

      Soft control for how verbose model output should be, used for GPT-5 models.

      - `"low"`

      - `"medium"`

      - `"high"`

  - `memory: Memory`

    Deprecated: Use `blocks` field instead. The in-context memory of the agent.

    - `blocks: Array<Block>`

      Memory blocks contained in the agent's in-context memory

      - `value: string`

        Value of the block.

      - `id?: string`

        The human-friendly ID of the Block

      - `base_template_id?: string | null`

        The base template id of the block.

      - `created_by_id?: string | null`

        The id of the user that made this Block.

      - `deployment_id?: string | null`

        The id of the deployment.

      - `description?: string | null`

        Description of the block.

      - `entity_id?: string | null`

        The id of the entity within the template.

      - `hidden?: boolean | null`

        If set to True, the block will be hidden.

      - `is_template?: boolean`

        Whether the block is a template (e.g. saved human/persona options).

      - `label?: string | null`

        Label of the block (e.g. 'human', 'persona') in the context window.

      - `last_updated_by_id?: string | null`

        The id of the user that last updated this Block.

      - `limit?: number`

        Character limit of the block.

      - `metadata?: Record<string, unknown> | null`

        Metadata of the block.

      - `preserve_on_migration?: boolean | null`

        Preserve the block on template migration.

      - `project_id?: string | null`

        The associated project id.

      - `read_only?: boolean`

        Whether the agent has read-only access to the block.

      - `tags?: Array<string> | null`

        The tags associated with the block.

      - `template_id?: string | null`

        The id of the template.

      - `template_name?: string | null`

        Name of the block if it is a template.

    - `agent_type?: AgentType | (string & {}) | null`

      Agent type controlling prompt rendering.

      - `AgentType = "memgpt_agent" | "memgpt_v2_agent" | "letta_v1_agent" | 6 more`

        Enum to represent the type of agent.

      - `(string & {})`

    - `file_blocks?: Array<FileBlock>`

      Special blocks representing the agent's in-context memory of an attached file

      - `file_id: string`

        Unique identifier of the file.

      - `is_open: boolean`

        True if the agent currently has the file open.

      - `source_id: string`

        Deprecated: Use `folder_id` field instead. Unique identifier of the source.

      - `value: string`

        Value of the block.

      - `id?: string`

        The human-friendly ID of the Block

      - `base_template_id?: string | null`

        The base template id of the block.

      - `created_by_id?: string | null`

        The id of the user that made this Block.

      - `deployment_id?: string | null`

        The id of the deployment.

      - `description?: string | null`

        Description of the block.

      - `entity_id?: string | null`

        The id of the entity within the template.

      - `hidden?: boolean | null`

        If set to True, the block will be hidden.

      - `is_template?: boolean`

        Whether the block is a template (e.g. saved human/persona options).

      - `label?: string | null`

        Label of the block (e.g. 'human', 'persona') in the context window.

      - `last_accessed_at?: string | null`

        UTC timestamp of the agent’s most recent access to this file. Any operations from the open, close, or search tools will update this field.

      - `last_updated_by_id?: string | null`

        The id of the user that last updated this Block.

      - `limit?: number`

        Character limit of the block.

      - `metadata?: Record<string, unknown> | null`

        Metadata of the block.

      - `preserve_on_migration?: boolean | null`

        Preserve the block on template migration.

      - `project_id?: string | null`

        The associated project id.

      - `read_only?: boolean`

        Whether the agent has read-only access to the block.

      - `tags?: Array<string> | null`

        The tags associated with the block.

      - `template_id?: string | null`

        The id of the template.

      - `template_name?: string | null`

        Name of the block if it is a template.

    - `git_enabled?: boolean`

      Whether this agent uses git-backed memory with structured labels.

    - `prompt_template?: string`

      Deprecated. Ignored for performance.

  - `name: string`

    The name of the agent.

  - `sources: Array<Source>`

    Deprecated: Use `folders` field instead. The sources used by the agent.

    - `id: string`

      The human-friendly ID of the Source

    - `embedding_config: EmbeddingConfig`

      The embedding configuration used by the source.

      - `embedding_dim: number`

        The dimension of the embedding.

      - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

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

      - `azure_deployment?: string | null`

        The Azure deployment for the model.

      - `azure_endpoint?: string | null`

        The Azure endpoint for the model.

      - `azure_version?: string | null`

        The Azure version for the model.

      - `batch_size?: number`

        The maximum batch size for processing embeddings.

      - `embedding_chunk_size?: number | null`

        The chunk size of the embedding.

      - `embedding_endpoint?: string | null`

        The endpoint for the model (`None` if local).

      - `handle?: string | null`

        The handle for this config, in the format provider/model-name.

    - `name: string`

      The name of the source.

    - `created_at?: string | null`

      The timestamp when the source was created.

    - `created_by_id?: string | null`

      The id of the user that made this Tool.

    - `description?: string | null`

      The description of the source.

    - `instructions?: string | null`

      Instructions for how to use the source.

    - `last_updated_by_id?: string | null`

      The id of the user that made this Tool.

    - `metadata?: Record<string, unknown> | null`

      Metadata associated with the source.

    - `updated_at?: string | null`

      The timestamp when the source was last updated.

    - `vector_db_provider?: VectorDBProvider`

      The vector database provider used for this source's passages

      - `"native"`

      - `"tpuf"`

      - `"pinecone"`

  - `system: string`

    The system prompt used by the agent.

  - `tags: Array<string>`

    The tags associated with the agent.

  - `tools: Array<Tool>`

    The tools used by the agent.

    - `id: string`

      The human-friendly ID of the Tool

    - `args_json_schema?: Record<string, unknown> | null`

      The args JSON schema of the function.

    - `created_by_id?: string | null`

      The id of the user that made this Tool.

    - `default_requires_approval?: boolean | null`

      Default value for whether or not executing this tool requires approval.

    - `description?: string | null`

      The description of the tool.

    - `enable_parallel_execution?: boolean | null`

      If set to True, then this tool will potentially be executed concurrently with other tools. Default False.

    - `json_schema?: Record<string, unknown> | null`

      The JSON schema of the function.

    - `last_updated_by_id?: string | null`

      The id of the user that made this Tool.

    - `metadata_?: Record<string, unknown> | null`

      A dictionary of additional metadata for the tool.

    - `name?: string | null`

      The name of the function.

    - `npm_requirements?: Array<NpmRequirement> | null`

      Optional list of npm packages required by this tool.

      - `name: string`

        Name of the npm package.

      - `version?: string | null`

        Optional version of the package, following semantic versioning.

    - `pip_requirements?: Array<PipRequirement> | null`

      Optional list of pip packages required by this tool.

      - `name: string`

        Name of the pip package.

      - `version?: string | null`

        Optional version of the package, following semantic versioning.

    - `project_id?: string | null`

      The project id of the tool.

    - `return_char_limit?: number`

      The maximum number of characters in the response.

    - `source_code?: string | null`

      The source code of the function.

    - `source_type?: string | null`

      The type of the source code.

    - `tags?: Array<string>`

      Metadata tags.

    - `tool_type?: ToolType`

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

  - `base_template_id?: string | null`

    The base template id of the agent.

  - `compaction_settings?: CompactionSettings | null`

    Configuration for conversation compaction / summarization.

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

          - `JsonSchemaResponseFormat`

            Response format for JSON schema-based responses.

          - `JsonObjectResponseFormat`

            Response format for JSON object responses.

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

  - `created_at?: string | null`

    The timestamp when the object was created.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `deployment_id?: string | null`

    The id of the deployment.

  - `description?: string | null`

    The description of the agent.

  - `embedding?: string | null`

    The embedding model handle used by the agent (format: provider/model-name).

  - `embedding_config?: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

  - `enable_sleeptime?: boolean | null`

    If set to True, memory management will move to a background agent thread.

  - `entity_id?: string | null`

    The id of the entity within the template.

  - `hidden?: boolean | null`

    If set to True, the agent will be hidden.

  - `identities?: Array<Identity>`

    The identities associated with this agent.

    - `id: string`

      The human-friendly ID of the Identity

    - `agent_ids: Array<string>`

      The IDs of the agents associated with the identity.

    - `block_ids: Array<string>`

      The IDs of the blocks associated with the identity.

    - `identifier_key: string`

      External, user-generated identifier key of the identity.

    - `identity_type: "org" | "user" | "other"`

      The type of the identity.

      - `"org"`

      - `"user"`

      - `"other"`

    - `name: string`

      The name of the identity.

    - `project_id?: string | null`

      The project id of the identity, if applicable.

    - `properties?: Array<Property>`

      List of properties associated with the identity

      - `key: string`

        The key of the property

      - `type: "string" | "number" | "boolean" | "json"`

        The type of the property

        - `"string"`

        - `"number"`

        - `"boolean"`

        - `"json"`

      - `value: string | number | boolean | Record<string, unknown>`

        The value of the property

        - `string`

        - `number`

        - `boolean`

        - `Record<string, unknown>`

  - `identity_ids?: Array<string>`

    Deprecated: Use `identities` field instead. The ids of the identities associated with this agent.

  - `last_run_completion?: string | null`

    The timestamp when the agent last completed a run.

  - `last_run_duration_ms?: number | null`

    The duration in milliseconds of the agent's last run.

  - `last_stop_reason?: StopReasonType | null`

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

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `managed_group?: ManagedGroup | null`

    The multi-agent group that this agent manages

    - `id: string`

      The id of the group. Assigned by the database.

    - `agent_ids: Array<string>`

    - `description: string`

    - `manager_type: "round_robin" | "supervisor" | "dynamic" | 3 more`

      - `"round_robin"`

      - `"supervisor"`

      - `"dynamic"`

      - `"sleeptime"`

      - `"voice_sleeptime"`

      - `"swarm"`

    - `base_template_id?: string | null`

      The base template id.

    - `deployment_id?: string | null`

      The id of the deployment.

    - `hidden?: boolean | null`

      If set to True, the group will be hidden.

    - `last_processed_message_id?: string | null`

    - `manager_agent_id?: string | null`

    - `max_message_buffer_length?: number | null`

      The desired maximum length of messages in the context window of the convo agent. This is a best effort, and may be off slightly due to user/assistant interleaving.

    - `max_turns?: number | null`

    - `min_message_buffer_length?: number | null`

      The desired minimum length of messages in the context window of the convo agent. This is a best effort, and may be off-by-one due to user/assistant interleaving.

    - `project_id?: string | null`

      The associated project id.

    - `shared_block_ids?: Array<string>`

    - `sleeptime_agent_frequency?: number | null`

    - `template_id?: string | null`

      The id of the template.

    - `termination_token?: string | null`

    - `turns_counter?: number | null`

  - `max_files_open?: number | null`

    Maximum number of files that can be open at once for this agent. Setting this too high may exceed the context window, which will break the agent.

  - `message_buffer_autoclear?: boolean`

    If set to True, the agent will not remember previous messages (though the agent will still retain state via core memory blocks and archival/recall memory). Not recommended unless you have an advanced use case.

  - `message_ids?: Array<string> | null`

    The ids of the messages in the agent's in-context memory.

  - `metadata?: Record<string, unknown> | null`

    The metadata of the agent.

  - `model?: string | null`

    The model handle used by the agent (format: provider/model-name).

  - `model_settings?: OpenAIModelSettings | SgLangModelSettings | AnthropicModelSettings | 14 more | null`

    The model settings used by the agent.

    - `OpenAIModelSettings`

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

    - `GoogleAIModelSettings`

    - `GoogleVertexModelSettings`

    - `AzureModelSettings`

      Azure OpenAI model configuration (OpenAI-compatible).

    - `XaiModelSettings`

      xAI model configuration (OpenAI-compatible).

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

    - `DeepseekModelSettings`

      Deepseek model configuration (OpenAI-compatible).

    - `TogetherModelSettings`

      Together AI model configuration (OpenAI-compatible).

    - `BedrockModelSettings`

      AWS Bedrock model configuration.

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

  - `multi_agent_group?: MultiAgentGroup | null`

    Deprecated: Use `managed_group` field instead. The multi-agent group that this agent manages.

    - `id: string`

      The id of the group. Assigned by the database.

    - `agent_ids: Array<string>`

    - `description: string`

    - `manager_type: "round_robin" | "supervisor" | "dynamic" | 3 more`

      - `"round_robin"`

      - `"supervisor"`

      - `"dynamic"`

      - `"sleeptime"`

      - `"voice_sleeptime"`

      - `"swarm"`

    - `base_template_id?: string | null`

      The base template id.

    - `deployment_id?: string | null`

      The id of the deployment.

    - `hidden?: boolean | null`

      If set to True, the group will be hidden.

    - `last_processed_message_id?: string | null`

    - `manager_agent_id?: string | null`

    - `max_message_buffer_length?: number | null`

      The desired maximum length of messages in the context window of the convo agent. This is a best effort, and may be off slightly due to user/assistant interleaving.

    - `max_turns?: number | null`

    - `min_message_buffer_length?: number | null`

      The desired minimum length of messages in the context window of the convo agent. This is a best effort, and may be off-by-one due to user/assistant interleaving.

    - `project_id?: string | null`

      The associated project id.

    - `shared_block_ids?: Array<string>`

    - `sleeptime_agent_frequency?: number | null`

    - `template_id?: string | null`

      The id of the template.

    - `termination_token?: string | null`

    - `turns_counter?: number | null`

  - `pending_approval?: ApprovalRequestMessage | null`

    A message representing a request for approval to call a tool (generated by the LLM to trigger tool execution).

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    tool_call (ToolCall): The tool call

    - `id: string`

    - `date: string`

    - `tool_call: ToolCall | ToolCallDelta`

      The tool call that has been requested by the llm to run

      - `ToolCall`

        - `arguments: string`

        - `name: string`

        - `tool_call_id: string`

      - `ToolCallDelta`

        - `arguments?: string | null`

        - `name?: string | null`

        - `tool_call_id?: string | null`

    - `is_err?: boolean | null`

    - `message_type?: "approval_request_message"`

      The type of the message.

      - `"approval_request_message"`

    - `name?: string | null`

    - `otid?: string | null`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id?: string | null`

    - `sender_id?: string | null`

    - `seq_id?: number | null`

    - `step_id?: string | null`

    - `tool_calls?: Array<ToolCall> | ToolCallDelta | null`

      The tool calls that have been requested by the llm to run, which are pending approval

      - `Array<ToolCall>`

        - `arguments: string`

        - `name: string`

        - `tool_call_id: string`

      - `ToolCallDelta`

  - `per_file_view_window_char_limit?: number | null`

    The per-file view window character limit for this agent. Setting this too high may exceed the context window, which will break the agent.

  - `project_id?: string | null`

    The id of the project the agent belongs to.

  - `response_format?: TextResponseFormat | JsonSchemaResponseFormat | JsonObjectResponseFormat | null`

    The response format used by the agent

    - `TextResponseFormat`

      Response format for plain text responses.

    - `JsonSchemaResponseFormat`

      Response format for JSON schema-based responses.

    - `JsonObjectResponseFormat`

      Response format for JSON object responses.

  - `secrets?: Array<AgentEnvironmentVariable>`

    The environment variables for tool execution specific to this agent.

    - `agent_id: string`

      The ID of the agent this environment variable belongs to.

    - `key: string`

      The name of the environment variable.

    - `value: string`

      The value of the environment variable.

    - `id?: string`

      The human-friendly ID of the Agent-env

    - `created_at?: string | null`

      The timestamp when the object was created.

    - `created_by_id?: string | null`

      The id of the user that made this object.

    - `description?: string | null`

      An optional description of the environment variable.

    - `last_updated_by_id?: string | null`

      The id of the user that made this object.

    - `updated_at?: string | null`

      The timestamp when the object was last updated.

    - `value_enc?: string | null`

      Encrypted secret value (stored as encrypted string)

  - `template_id?: string | null`

    The id of the template the agent belongs to.

  - `timezone?: string | null`

    The timezone of the agent (IANA format).

  - `tool_exec_environment_variables?: Array<AgentEnvironmentVariable>`

    Deprecated: use `secrets` field instead.

    - `agent_id: string`

      The ID of the agent this environment variable belongs to.

    - `key: string`

      The name of the environment variable.

    - `value: string`

      The value of the environment variable.

    - `id?: string`

      The human-friendly ID of the Agent-env

    - `created_at?: string | null`

      The timestamp when the object was created.

    - `created_by_id?: string | null`

      The id of the user that made this object.

    - `description?: string | null`

      An optional description of the environment variable.

    - `last_updated_by_id?: string | null`

      The id of the user that made this object.

    - `updated_at?: string | null`

      The timestamp when the object was last updated.

    - `value_enc?: string | null`

      Encrypted secret value (stored as encrypted string)

  - `tool_rules?: Array<ChildToolRule | InitToolRule | TerminalToolRule | 6 more> | null`

    The list of tool rules.

    - `ChildToolRule`

      A ToolRule represents a tool that can be invoked by the agent.

      - `children: Array<string>`

        The children tools that can be invoked.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `child_arg_nodes?: Array<ChildArgNode> | null`

        Optional list of typed child argument overrides. Each node must reference a child in 'children'.

        - `name: string`

          The name of the child tool to invoke next.

        - `args?: Record<string, unknown> | null`

          Optional prefilled arguments for this child tool. Keys must match the tool's parameter names and values must satisfy the tool's JSON schema. Supports partial prefill; non-overlapping parameters are left to the model.

      - `prompt_template?: string | null`

        Optional template string (ignored).

      - `type?: "constrain_child_tools"`

        - `"constrain_child_tools"`

    - `InitToolRule`

      Represents the initial tool rule configuration.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `args?: Record<string, unknown> | null`

        Optional prefilled arguments for this tool. When present, these values will override any LLM-provided arguments with the same keys during invocation. Keys must match the tool's parameter names and values must satisfy the tool's JSON schema. Supports partial prefill; non-overlapping parameters are left to the model.

      - `prompt_template?: string | null`

        Optional template string (ignored). Rendering uses fast built-in formatting for performance.

      - `type?: "run_first"`

        - `"run_first"`

    - `TerminalToolRule`

      Represents a terminal tool rule configuration where if this tool gets called, it must end the agent loop.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `prompt_template?: string | null`

        Optional template string (ignored).

      - `type?: "exit_loop"`

        - `"exit_loop"`

    - `ConditionalToolRule`

      A ToolRule that conditionally maps to different child tools based on the output.

      - `child_output_mapping: Record<string, string>`

        The output case to check for mapping

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `default_child?: string | null`

        The default child tool to be called. If None, any tool can be called.

      - `prompt_template?: string | null`

        Optional template string (ignored).

      - `require_output_mapping?: boolean`

        Whether to throw an error when output doesn't match any case

      - `type?: "conditional"`

        - `"conditional"`

    - `ContinueToolRule`

      Represents a tool rule configuration where if this tool gets called, it must continue the agent loop.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `prompt_template?: string | null`

        Optional template string (ignored).

      - `type?: "continue_loop"`

        - `"continue_loop"`

    - `RequiredBeforeExitToolRule`

      Represents a tool rule configuration where this tool must be called before the agent loop can exit.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `prompt_template?: string | null`

        Optional template string (ignored).

      - `type?: "required_before_exit"`

        - `"required_before_exit"`

    - `MaxCountPerStepToolRule`

      Represents a tool rule configuration which constrains the total number of times this tool can be invoked in a single step.

      - `max_count_limit: number`

        The max limit for the total number of times this tool can be invoked in a single step.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `prompt_template?: string | null`

        Optional template string (ignored).

      - `type?: "max_count_per_step"`

        - `"max_count_per_step"`

    - `ParentToolRule`

      A ToolRule that only allows a child tool to be called if the parent has been called.

      - `children: Array<string>`

        The children tools that can be invoked.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `prompt_template?: string | null`

        Optional template string (ignored).

      - `type?: "parent_last_tool"`

        - `"parent_last_tool"`

    - `RequiresApprovalToolRule`

      Represents a tool rule configuration which requires approval before the tool can be invoked.

      - `tool_name: string`

        The name of the tool. Must exist in the database for the user's organization.

      - `prompt_template?: string | null`

        Optional template string (ignored). Rendering uses fast built-in formatting for performance.

      - `type?: "requires_approval"`

        - `"requires_approval"`

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const agentState = await client.agents.blocks.detach('block-123e4567-e89b-42d3-8456-426614174000', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(agentState.id);
```

#### Response

```json
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
```
