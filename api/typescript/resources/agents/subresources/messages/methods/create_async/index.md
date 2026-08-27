## Create Message Async

`client.agents.messages.createAsync(stringagentID, MessageCreateAsyncParamsbody, RequestOptionsoptions?): Run`

**post** `/v1/agents/{agent_id}/messages/async`

Asynchronously process a user message and return a run object.
The actual processing happens in the background, and the status can be checked using the run ID.

This is "asynchronous" in the sense that it's a background run and explicitly must be fetched by the run ID.

**Note:** Sending multiple concurrent requests to the same agent can lead to undefined behavior.
Each agent processes messages sequentially, and concurrent requests may interleave in unexpected ways.
Wait for each request to complete before sending the next one. Use separate agents or conversations for parallel processing.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `body: MessageCreateAsyncParams`

  - `assistant_message_tool_kwarg?: string`

    The name of the message argument in the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

  - `assistant_message_tool_name?: string`

    The name of the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

  - `callback_url?: string | null`

    Optional callback URL to POST to when the job completes

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

  - `top_logprobs?: number | null`

    Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

  - `use_assistant_message?: boolean`

    Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

### Returns

- `Run`

  Representation of a run - a conversation or processing session for an agent. Runs track when agents process messages and maintain the relationship between agents, steps, and messages.

  - `id: string`

    The human-friendly ID of the Run

  - `agent_id: string`

    The unique identifier of the agent associated with the run.

  - `background?: boolean | null`

    Whether the run was created in background mode.

  - `base_template_id?: string | null`

    The base template ID that the run belongs to.

  - `callback_error?: string | null`

    Optional error message from attempting to POST the callback endpoint.

  - `callback_sent_at?: string | null`

    Timestamp when the callback was last attempted.

  - `callback_status_code?: number | null`

    HTTP status code returned by the callback endpoint.

  - `callback_url?: string | null`

    If set, POST to this URL when the run completes.

  - `completed_at?: string | null`

    The timestamp when the run was completed.

  - `conversation_id?: string | null`

    The unique identifier of the conversation associated with the run.

  - `created_at?: string`

    The timestamp when the run was created.

  - `metadata?: Record<string, unknown> | null`

    Additional metadata for the run.

  - `request_config?: RequestConfig | null`

    The request configuration for the run.

    - `assistant_message_tool_kwarg?: string`

      The name of the message argument in the designated message tool.

    - `assistant_message_tool_name?: string`

      The name of the designated message tool.

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

    - `use_assistant_message?: boolean`

      Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects.

  - `status?: "created" | "running" | "completed" | 2 more`

    The current status of the run.

    - `"created"`

    - `"running"`

    - `"completed"`

    - `"failed"`

    - `"cancelled"`

  - `stop_reason?: StopReasonType | null`

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

  - `total_duration_ns?: number | null`

    Total run duration in nanoseconds

  - `ttft_ns?: number | null`

    Time to first token for a run in nanoseconds

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const run = await client.agents.messages.createAsync('agent-123e4567-e89b-42d3-8456-426614174000');

console.log(run.id);
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
