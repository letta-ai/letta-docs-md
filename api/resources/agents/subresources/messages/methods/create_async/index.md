## Create Message Async

**post** `/v1/agents/{agent_id}/messages/async`

Asynchronously process a user message and return a run object.
The actual processing happens in the background, and the status can be checked using the run ID.

This is "asynchronous" in the sense that it's a background run and explicitly must be fetched by the run ID.

**Note:** Sending multiple concurrent requests to the same agent can lead to undefined behavior.
Each agent processes messages sequentially, and concurrent requests may interleave in unexpected ways.
Wait for each request to complete before sending the next one. Use separate agents or conversations for parallel processing.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Body Parameters

- `assistant_message_tool_kwarg: optional string`

  The name of the message argument in the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

- `assistant_message_tool_name: optional string`

  The name of the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

- `callback_url: optional string`

  Optional callback URL to POST to when the job completes

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

- `top_logprobs: optional number`

  Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

- `use_assistant_message: optional boolean`

  Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

### Returns

- `Run object { id, agent_id, background, 14 more }`

  Representation of a run - a conversation or processing session for an agent. Runs track when agents process messages and maintain the relationship between agents, steps, and messages.

  - `id: string`

    The human-friendly ID of the Run

  - `agent_id: string`

    The unique identifier of the agent associated with the run.

  - `background: optional boolean`

    Whether the run was created in background mode.

  - `base_template_id: optional string`

    The base template ID that the run belongs to.

  - `callback_error: optional string`

    Optional error message from attempting to POST the callback endpoint.

  - `callback_sent_at: optional string`

    Timestamp when the callback was last attempted.

  - `callback_status_code: optional number`

    HTTP status code returned by the callback endpoint.

  - `callback_url: optional string`

    If set, POST to this URL when the run completes.

  - `completed_at: optional string`

    The timestamp when the run was completed.

  - `conversation_id: optional string`

    The unique identifier of the conversation associated with the run.

  - `created_at: optional string`

    The timestamp when the run was created.

  - `metadata: optional map[unknown]`

    Additional metadata for the run.

  - `request_config: optional object { assistant_message_tool_kwarg, assistant_message_tool_name, include_return_message_types, use_assistant_message }`

    The request configuration for the run.

    - `assistant_message_tool_kwarg: optional string`

      The name of the message argument in the designated message tool.

    - `assistant_message_tool_name: optional string`

      The name of the designated message tool.

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

    - `use_assistant_message: optional boolean`

      Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects.

  - `status: optional "created" or "running" or "completed" or 2 more`

    The current status of the run.

    - `"created"`

    - `"running"`

    - `"completed"`

    - `"failed"`

    - `"cancelled"`

  - `stop_reason: optional StopReasonType`

    The reason why the run was stopped.

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

  - `total_duration_ns: optional number`

    Total run duration in nanoseconds

  - `ttft_ns: optional number`

    Time to first token for a run in nanoseconds

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/messages/async \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{}'
```

#### Response

```json
{
  "id": "run-123e4567-e89b-12d3-a456-426614174000",
  "agent_id": "agent_id",
  "background": true,
  "base_template_id": "base_template_id",
  "callback_error": "callback_error",
  "callback_sent_at": "2019-12-27T18:11:19.117Z",
  "callback_status_code": 0,
  "callback_url": "callback_url",
  "completed_at": "2019-12-27T18:11:19.117Z",
  "conversation_id": "conversation_id",
  "created_at": "2019-12-27T18:11:19.117Z",
  "metadata": {
    "foo": "bar"
  },
  "request_config": {
    "assistant_message_tool_kwarg": "assistant_message_tool_kwarg",
    "assistant_message_tool_name": "assistant_message_tool_name",
    "include_return_message_types": [
      "system_message"
    ],
    "use_assistant_message": true
  },
  "status": "created",
  "stop_reason": "end_turn",
  "total_duration_ns": 0,
  "ttft_ns": 0
}
```
