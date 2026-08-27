## Create Message

`client.agents.messages.create(stringagentID, MessageCreateParamsbody, RequestOptionsoptions?): LettaResponse | Stream<LettaStreamingResponse>`

**post** `/v1/agents/{agent_id}/messages`

Process a user message and return the agent's response.
This endpoint accepts a message from a user and processes it through the agent.

**Note:** Sending multiple concurrent requests to the same agent can lead to undefined behavior.
Each agent processes messages sequentially, and concurrent requests may interleave in unexpected ways.
Wait for each request to complete before sending the next one. Use separate agents or conversations for parallel processing.

The response format is controlled by the `streaming` field in the request body:

- If `streaming=false` (default): Returns a complete LettaResponse with all messages
- If `streaming=true`: Returns a Server-Sent Events (SSE) stream

Additional streaming options (only used when streaming=true):

- `stream_tokens`: Stream individual tokens instead of complete steps
- `include_pings`: Include keepalive pings to prevent connection timeouts
- `background`: Process the request in the background

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `MessageCreateParams = MessageCreateParamsNonStreaming | MessageCreateParamsStreaming`

  - `MessageCreateParamsBase`

    - `assistant_message_tool_kwarg?: string`

      The name of the message argument in the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

    - `assistant_message_tool_name?: string`

      The name of the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

    - `background?: boolean`

      Whether to process the request in the background (only used when streaming=true).

    - `client_skills?: Array<ClientSkill> | null`

      Client-side skills available in the environment. These are rendered in the system prompt's available skills section alongside agent-scoped skills from MemFS.

      - `description: string`

        Description of what the skill does

      - `location: string`

        Path or location hint for the skill (e.g. skills/my-skill/SKILL.md)

      - `name: string`

        The name of the skill

    - `client_tools?: Array<ClientTool> | null`

      Client-side tools that the agent can call. When the agent calls a client-side tool, execution pauses and returns control to the client to execute the tool and provide the result via a ToolReturn.

      - `name: string`

        The name of the tool function

      - `description?: string | null`

        Description of what the tool does

      - `parameters?: Record<string, unknown> | null`

        JSON Schema for the function parameters

    - `enable_thinking?: string`

      If set to True, enables reasoning before responses or tool calls from the agent.

    - `include_compaction_messages?: boolean`

      If True, compaction events emit structured `SummaryMessage` and `EventMessage` types. If False (default), compaction messages are not included in the response.

    - `include_pings?: boolean`

      Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts (only used when streaming=true).

    - `include_return_message_types?: Array<MessageType> | null`

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

    - `input?: string | Array<TextContent | ImageContent | ToolCallContent | 5 more> | null`

      Syntactic sugar for a single user message. Equivalent to messages=[{'role': 'user', 'content': input}].

      - `string`

      - `Array<TextContent | ImageContent | ToolCallContent | 5 more>`

        - `TextContent`

          - `text: string`

            The text content of the message.

          - `signature?: string | null`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type?: "text"`

            The type of the message.

            - `"text"`

        - `ImageContent`

          - `source: URLImage | Base64Image | LettaImage`

            The source of the image.

            - `URLImage`

              - `url: string`

                The URL of the image.

              - `type?: "url"`

                The source type for the image.

                - `"url"`

            - `Base64Image`

              - `data: string`

                The base64 encoded image data.

              - `media_type: string`

                The media type for the image.

              - `detail?: string | null`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `type?: "base64"`

                The source type for the image.

                - `"base64"`

            - `LettaImage`

              - `file_id: string`

                The unique identifier of the image file persisted in storage.

              - `data?: string | null`

                The base64 encoded image data.

              - `detail?: string | null`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `media_type?: string | null`

                The media type for the image.

              - `type?: "letta"`

                The source type for the image.

                - `"letta"`

          - `type?: "image"`

            The type of the message.

            - `"image"`

        - `ToolCallContent`

          - `id: string`

            A unique identifier for this specific tool call instance.

          - `input: Record<string, unknown>`

            The parameters being passed to the tool, structured as a dictionary of parameter names to values.

          - `name: string`

            The name of the tool being called.

          - `signature?: string | null`

            Stores a unique identifier for any reasoning associated with this tool call.

          - `type?: "tool_call"`

            Indicates this content represents a tool call event.

            - `"tool_call"`

        - `ToolReturnContent`

          - `content: string`

            The content returned by the tool execution.

          - `is_error: boolean`

            Indicates whether the tool execution resulted in an error.

          - `tool_call_id: string`

            References the ID of the ToolCallContent that initiated this tool call.

          - `type?: "tool_return"`

            Indicates this content represents a tool return event.

            - `"tool_return"`

        - `ReasoningContent`

          Sent via the Anthropic Messages API

          - `is_native: boolean`

            Whether the reasoning content was generated by a reasoner model that processed this step.

          - `reasoning: string`

            The intermediate reasoning or thought process content.

          - `signature?: string | null`

            A unique identifier for this reasoning step.

          - `type?: "reasoning"`

            Indicates this is a reasoning/intermediate step.

            - `"reasoning"`

        - `RedactedReasoningContent`

          Sent via the Anthropic Messages API

          - `data: string`

            The redacted or filtered intermediate reasoning content.

          - `type?: "redacted_reasoning"`

            Indicates this is a redacted thinking step.

            - `"redacted_reasoning"`

        - `OmittedReasoningContent`

          A placeholder for reasoning content we know is present, but isn't returned by the provider (e.g. OpenAI GPT-5 on ChatCompletions)

          - `signature?: string | null`

            A unique identifier for this reasoning step.

          - `type?: "omitted_reasoning"`

            Indicates this is an omitted reasoning step.

            - `"omitted_reasoning"`

        - `SummarizedReasoningContent`

          The style of reasoning content returned by the OpenAI Responses API

          - `id: string`

            The unique identifier for this reasoning step.

          - `summary: Array<Summary>`

            Summaries of the reasoning content.

            - `index: number`

              The index of the summary part.

            - `text: string`

              The text of the summary part.

          - `encrypted_content?: string`

            The encrypted reasoning content.

          - `type?: "summarized_reasoning"`

            Indicates this is a summarized reasoning step.

            - `"summarized_reasoning"`

    - `max_steps?: number`

      Maximum number of steps the agent should take to process the request.

    - `messages?: Array<MessageCreate | ApprovalCreate | ToolReturnCreate> | null`

      The messages to be sent to the agent.

      - `MessageCreate`

        Request to create a message

        - `content: Array<LettaMessageContentUnion> | string`

          The content of the message.

          - `Array<LettaMessageContentUnion>`

            - `TextContent`

            - `ImageContent`

            - `ToolCallContent`

            - `ToolReturnContent`

            - `ReasoningContent`

              Sent via the Anthropic Messages API

            - `RedactedReasoningContent`

              Sent via the Anthropic Messages API

            - `OmittedReasoningContent`

              A placeholder for reasoning content we know is present, but isn't returned by the provider (e.g. OpenAI GPT-5 on ChatCompletions)

          - `string`

        - `role: "user" | "system" | "assistant"`

          The role of the participant.

          - `"user"`

          - `"system"`

          - `"assistant"`

        - `batch_item_id?: string | null`

          The id of the LLMBatchItem that this message is associated with

        - `group_id?: string | null`

          The multi-agent group that the message was sent in

        - `name?: string | null`

          The name of the participant.

        - `otid?: string | null`

          The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

        - `sender_id?: string | null`

          The id of the sender of the message, can be an identity id or agent id

        - `type?: "message" | null`

          The message type to be created.

          - `"message"`

      - `ApprovalCreate`

        Input to approve or deny a tool call request

        - `approval_request_id?: string | null`

          The message ID of the approval request

        - `approvals?: Array<ApprovalReturn | ToolReturn> | null`

          The list of approval responses

          - `ApprovalReturn`

            - `approve: boolean`

              Whether the tool has been approved

            - `tool_call_id: string`

              The ID of the tool call that corresponds to this approval

            - `reason?: string | null`

              An optional explanation for the provided approval status

            - `type?: "approval"`

              The message type to be created.

              - `"approval"`

          - `ToolReturn`

            - `status: "success" | "error"`

              - `"success"`

              - `"error"`

            - `tool_call_id: string`

            - `tool_return: Array<TextContent | ImageContent> | string`

              The tool return value - either a string or list of content parts (text/image)

              - `Array<TextContent | ImageContent>`

                - `TextContent`

                - `ImageContent`

              - `string`

            - `stderr?: Array<string> | null`

            - `stdout?: Array<string> | null`

            - `type?: "tool"`

              The message type to be created.

              - `"tool"`

        - `approve?: boolean | null`

          Whether the tool has been approved

        - `group_id?: string | null`

          The multi-agent group that the message was sent in

        - `otid?: string | null`

          The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

        - `reason?: string | null`

          An optional explanation for the provided approval status

        - `type?: "approval"`

          The message type to be created.

          - `"approval"`

      - `ToolReturnCreate`

        Submit tool return(s) from client-side tool execution.

        This is the preferred way to send tool results back to the agent after
        client-side tool execution. It is equivalent to sending an ApprovalCreate
        with tool return approvals, but provides a cleaner API for the common case.

        - `tool_returns: Array<ToolReturn>`

          List of tool returns from client-side execution

          - `status: "success" | "error"`

          - `tool_call_id: string`

          - `tool_return: Array<TextContent | ImageContent> | string`

            The tool return value - either a string or list of content parts (text/image)

          - `stderr?: Array<string> | null`

          - `stdout?: Array<string> | null`

          - `type?: "tool"`

            The message type to be created.

        - `group_id?: string | null`

          The multi-agent group that the message was sent in

        - `otid?: string | null`

          The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

        - `type?: "tool_return"`

          The message type to be created.

          - `"tool_return"`

    - `override_model?: string | null`

      Model handle to use for this request instead of the agent's default model. This allows sending a message to a different model without changing the agent's configuration.

    - `override_system?: string | null`

      Optional per-request system prompt override. When set, this is passed directly to the underlying LLM request and bypasses the persisted/compiled system message for that request.

    - `return_logprobs?: boolean`

      If True, returns log probabilities of the output tokens in the response. Useful for RL training. Only supported for OpenAI-compatible providers (including SGLang).

    - `return_token_ids?: boolean`

      If True, returns token IDs and logprobs for ALL LLM generations in the agent step, not just the last one. Uses SGLang native /generate endpoint. Returns 'turns' field with TurnTokenData for each assistant/tool turn. Required for proper multi-turn RL training with loss masking.

    - `stream_tokens?: boolean`

      Flag to determine if individual tokens should be streamed, rather than streaming per step (only used when streaming=true).

    - `streaming?: false`

      If True, returns a streaming response (Server-Sent Events). If False (default), returns a complete response.

      - `false`

    - `top_logprobs?: number | null`

      Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

    - `use_assistant_message?: boolean`

      Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

  - `MessageCreateParamsNonStreaming extends MessageCreateParamsBase`

    - `streaming?: false`

      If True, returns a streaming response (Server-Sent Events). If False (default), returns a complete response.

  - `MessageCreateParamsStreaming extends MessageCreateParamsBase`

    - `streaming: true`

      If True, returns a streaming response (Server-Sent Events). If False (default), returns a complete response.

      - `true`

### Returns

- `LettaResponse`

  Response object from an agent interaction, consisting of the new messages generated by the agent and usage statistics.
  The type of the returned messages can be either `Message` or `LettaMessage`, depending on what was specified in the request.

  Attributes:
  messages (List[Union[Message, LettaMessage]]): The messages returned by the agent.
  usage (LettaUsageStatistics): The usage statistics

  - `messages: Array<Message>`

    The messages returned by the agent.

    - `SystemMessage`

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

      - `is_err?: boolean | null`

      - `message_type?: "system_message"`

        The type of the message.

        - `"system_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

    - `UserMessage`

      A message sent by the user. Never streamed back on a response, only used for cursor pagination.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      content (Union[str, List[LettaUserMessageContentUnion]]): The message content sent by the user (can be a string or an array of multi-modal content parts)

      - `id: string`

      - `content: Array<LettaUserMessageContentUnion> | string`

        The message content sent by the user (can be a string or an array of multi-modal content parts)

        - `Array<LettaUserMessageContentUnion>`

          - `TextContent`

            - `text: string`

              The text content of the message.

            - `signature?: string | null`

              Stores a unique identifier for any reasoning associated with this text content.

            - `type?: "text"`

              The type of the message.

              - `"text"`

          - `ImageContent`

            - `source: URLImage | Base64Image | LettaImage`

              The source of the image.

              - `URLImage`

                - `url: string`

                  The URL of the image.

                - `type?: "url"`

                  The source type for the image.

                  - `"url"`

              - `Base64Image`

                - `data: string`

                  The base64 encoded image data.

                - `media_type: string`

                  The media type for the image.

                - `detail?: string | null`

                  What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

                - `type?: "base64"`

                  The source type for the image.

                  - `"base64"`

              - `LettaImage`

                - `file_id: string`

                  The unique identifier of the image file persisted in storage.

                - `data?: string | null`

                  The base64 encoded image data.

                - `detail?: string | null`

                  What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

                - `media_type?: string | null`

                  The media type for the image.

                - `type?: "letta"`

                  The source type for the image.

                  - `"letta"`

            - `type?: "image"`

              The type of the message.

              - `"image"`

        - `string`

      - `date: string`

      - `is_err?: boolean | null`

      - `message_type?: "user_message"`

        The type of the message.

        - `"user_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

    - `ReasoningMessage`

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

      - `is_err?: boolean | null`

      - `message_type?: "reasoning_message"`

        The type of the message.

        - `"reasoning_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `signature?: string | null`

      - `source?: "reasoner_model" | "non_reasoner_model"`

        - `"reasoner_model"`

        - `"non_reasoner_model"`

      - `step_id?: string | null`

    - `HiddenReasoningMessage`

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

      - `state: "redacted" | "omitted"`

        - `"redacted"`

        - `"omitted"`

      - `hidden_reasoning?: string | null`

      - `is_err?: boolean | null`

      - `message_type?: "hidden_reasoning_message"`

        The type of the message.

        - `"hidden_reasoning_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

    - `ToolCallMessage`

      A message representing a request to call a tool (generated by the LLM to trigger tool execution).

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      tool_call (Union[ToolCall, ToolCallDelta]): The tool call

      - `id: string`

      - `date: string`

      - `tool_call: ToolCall | ToolCallDelta`

        - `ToolCall`

          - `arguments: string`

          - `name: string`

          - `tool_call_id: string`

        - `ToolCallDelta`

          - `arguments?: string | null`

          - `name?: string | null`

          - `tool_call_id?: string | null`

      - `is_err?: boolean | null`

      - `message_type?: "tool_call_message"`

        The type of the message.

        - `"tool_call_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

      - `tool_calls?: Array<ToolCall> | ToolCallDelta | null`

        - `Array<ToolCall>`

          - `arguments: string`

          - `name: string`

          - `tool_call_id: string`

        - `ToolCallDelta`

    - `ToolReturnMessage`

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

      - `status: "success" | "error"`

        - `"success"`

        - `"error"`

      - `tool_call_id: string`

      - `tool_return: string`

      - `is_err?: boolean | null`

      - `message_type?: "tool_return_message"`

        The type of the message.

        - `"tool_return_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `stderr?: Array<string> | null`

      - `stdout?: Array<string> | null`

      - `step_id?: string | null`

      - `tool_returns?: Array<ToolReturn> | null`

        - `status: "success" | "error"`

          - `"success"`

          - `"error"`

        - `tool_call_id: string`

        - `tool_return: Array<TextContent | ImageContent> | string`

          The tool return value - either a string or list of content parts (text/image)

          - `Array<TextContent | ImageContent>`

            - `TextContent`

            - `ImageContent`

          - `string`

        - `stderr?: Array<string> | null`

        - `stdout?: Array<string> | null`

        - `type?: "tool"`

          The message type to be created.

          - `"tool"`

    - `AssistantMessage`

      A message sent by the LLM in response to user input. Used in the LLM context.

      Args:
      id (str): The ID of the message
      date (datetime): The date the message was created in ISO format
      name (Optional[str]): The name of the sender of the message
      content (Union[str, List[LettaAssistantMessageContentUnion]]): The message content sent by the agent (can be a string or an array of content parts)

      - `id: string`

      - `content: Array<LettaAssistantMessageContentUnion> | string`

        The message content sent by the agent (can be a string or an array of content parts)

        - `Array<LettaAssistantMessageContentUnion>`

          - `text: string`

            The text content of the message.

          - `signature?: string | null`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type?: "text"`

            The type of the message.

            - `"text"`

        - `string`

      - `date: string`

      - `is_err?: boolean | null`

      - `message_type?: "assistant_message"`

        The type of the message.

        - `"assistant_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

    - `ApprovalRequestMessage`

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

        - `ToolCallDelta`

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

    - `ApprovalResponseMessage`

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

      - `approval_request_id?: string | null`

        The message ID of the approval request

      - `approvals?: Array<ApprovalReturn | ToolReturn> | null`

        The list of approval responses

        - `ApprovalReturn`

          - `approve: boolean`

            Whether the tool has been approved

          - `tool_call_id: string`

            The ID of the tool call that corresponds to this approval

          - `reason?: string | null`

            An optional explanation for the provided approval status

          - `type?: "approval"`

            The message type to be created.

            - `"approval"`

        - `ToolReturn`

          - `status: "success" | "error"`

          - `tool_call_id: string`

          - `tool_return: Array<TextContent | ImageContent> | string`

            The tool return value - either a string or list of content parts (text/image)

          - `stderr?: Array<string> | null`

          - `stdout?: Array<string> | null`

          - `type?: "tool"`

            The message type to be created.

      - `approve?: boolean | null`

        Whether the tool has been approved

      - `is_err?: boolean | null`

      - `message_type?: "approval_response_message"`

        The type of the message.

        - `"approval_response_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `reason?: string | null`

        An optional explanation for the provided approval status

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

    - `SummaryMessage`

      A message representing a summary of the conversation. Sent to the LLM as a user or system message depending on the provider.

      - `id: string`

      - `date: string`

      - `summary: string`

      - `compaction_stats?: CompactionStats | null`

        Statistics about a memory compaction operation.

        - `context_window: number`

          The model's context window size

        - `messages_count_after: number`

          Number of messages after compaction

        - `messages_count_before: number`

          Number of messages before compaction

        - `trigger: string`

          What triggered the compaction (e.g., 'context_window_exceeded', 'post_step_context_check')

        - `context_tokens_after?: number | null`

          Token count after compaction (message tokens only, does not include tool definitions)

        - `context_tokens_before?: number | null`

          Token count before compaction (from LLM usage stats, includes full context sent to LLM)

      - `is_err?: boolean | null`

      - `message_type?: "summary_message"`

        - `"summary_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

    - `EventMessage`

      A message for notifying the developer that an event that has occured (e.g. a compaction). Events are NOT part of the context window.

      - `id: string`

      - `date: string`

      - `event_data: Record<string, unknown>`

      - `event_type: "compaction"`

        - `"compaction"`

      - `is_err?: boolean | null`

      - `message_type?: "event_message"`

        - `"event_message"`

      - `name?: string | null`

      - `otid?: string | null`

        The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

      - `run_id?: string | null`

      - `sender_id?: string | null`

      - `seq_id?: number | null`

      - `step_id?: string | null`

  - `stop_reason: StopReason`

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

    - `message_type?: "stop_reason"`

      The type of the message.

      - `"stop_reason"`

  - `usage: Usage`

    The usage statistics of the agent.

    - `cache_write_tokens?: number | null`

      The number of input tokens written to cache (Anthropic only). None if not reported by provider.

    - `cached_input_tokens?: number | null`

      The number of input tokens served from cache. None if not reported by provider.

    - `completion_tokens?: number`

      The number of tokens generated by the agent.

    - `context_tokens?: number | null`

      Estimate of tokens currently in the context window.

    - `message_type?: "usage_statistics"`

      - `"usage_statistics"`

    - `prompt_tokens?: number`

      The number of tokens in the prompt.

    - `reasoning_tokens?: number | null`

      The number of reasoning/thinking tokens generated. None if not reported by provider.

    - `run_ids?: Array<string> | null`

      The background task run IDs associated with the agent interaction

    - `step_count?: number`

      The number of steps taken by the agent.

    - `total_tokens?: number`

      The total number of tokens processed by the agent.

  - `logprobs?: Logprobs | null`

    Log probabilities of the output tokens from the last LLM call. Only present if return_logprobs was enabled.

    - `content?: Array<Content> | null`

      - `token: string`

      - `logprob: number`

      - `top_logprobs: Array<TopLogprob>`

        - `token: string`

        - `logprob: number`

        - `bytes?: Array<number> | null`

      - `bytes?: Array<number> | null`

    - `refusal?: Array<Refusal> | null`

      - `token: string`

      - `logprob: number`

      - `top_logprobs: Array<TopLogprob>`

        - `token: string`

        - `logprob: number`

        - `bytes?: Array<number> | null`

      - `bytes?: Array<number> | null`

  - `turns?: Array<Turn> | null`

    Token data for all LLM generations in multi-turn agent interaction. Includes token IDs and logprobs for each assistant turn, plus tool result content. Only present if return_token_ids was enabled. Used for RL training with loss masking.

    - `role: "assistant" | "tool"`

      Role of this turn: 'assistant' for LLM generations (trainable), 'tool' for tool results (non-trainable).

      - `"assistant"`

      - `"tool"`

    - `content?: string | null`

      Text content. For tool turns, client tokenizes this with loss_mask=0.

    - `output_ids?: Array<number> | null`

      Token IDs from SGLang native endpoint. Only present for assistant turns.

    - `output_token_logprobs?: Array<Array<unknown>> | null`

      Logprobs from SGLang: [[logprob, token_id, top_logprob_or_null], ...]. Only present for assistant turns.

    - `tool_name?: string | null`

      Name of the tool called. Only present for tool turns.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const lettaResponse = await client.agents.messages.create(
  'agent-123e4567-e89b-42d3-8456-426614174000',
);

console.log(lettaResponse.messages);
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
