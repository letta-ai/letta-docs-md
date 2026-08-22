# Runs

## List Runs

`client.runs.list(RunListParamsquery?, RequestOptionsoptions?): ArrayPage<Run>`

**get** `/v1/runs/`

List all runs.

### Parameters

- `query: RunListParams`

  - `active?: boolean`

    Filter for active runs.

  - `after?: string | null`

    Cursor for pagination (run ID). Returns results relative to this ID in the specified sort order. Expected format: 'run-<uuid4>'

  - `agent_id?: string | null`

    The unique identifier of the agent associated with the run.

  - `agent_ids?: Array<string> | null`

    The unique identifiers of the agents associated with the run. Deprecated in favor of agent_id field.

  - `ascending?: boolean`

    Whether to sort agents oldest to newest (True) or newest to oldest (False, default). Deprecated in favor of order field.

  - `background?: boolean | null`

    If True, filters for runs that were created in background mode.

  - `before?: string | null`

    Cursor for pagination (run ID). Returns results relative to this ID in the specified sort order. Expected format: 'run-<uuid4>'

  - `conversation_id?: string | null`

    Filter runs by conversation ID.

  - `limit?: number | null`

    Maximum number of runs to return

  - `order?: "asc" | "desc"`

    Sort order for runs by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

  - `statuses?: Array<string> | null`

    Filter runs by status. Can specify multiple statuses.

  - `stop_reason?: StopReasonType | null`

    Filter runs by stop reason.

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

// Automatically fetches more pages as needed.
for await (const run of client.runs.list()) {
  console.log(run.id);
}
```

#### Response

```json
[
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
]
```

## Retrieve Run

`client.runs.retrieve(stringrunID, RequestOptionsoptions?): Run`

**get** `/v1/runs/{run_id}`

Get the status of a run.

### Parameters

- `runID: string`

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

const run = await client.runs.retrieve('run_id');

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

## Domain Types

### Job

- `Job`

  Representation of offline jobs, used for tracking status of data loading tasks (involving parsing and embedding files).

  - `id?: string`

    The human-friendly ID of the Job

  - `agent_id?: string | null`

    The agent associated with this job/run.

  - `background?: boolean | null`

    Whether the job was created in background mode.

  - `callback_error?: string | null`

    Optional error message from attempting to POST the callback endpoint.

  - `callback_sent_at?: string | null`

    Timestamp when the callback was last attempted.

  - `callback_status_code?: number | null`

    HTTP status code returned by the callback endpoint.

  - `callback_url?: string | null`

    If set, POST to this URL when the job completes.

  - `completed_at?: string | null`

    The unix timestamp of when the job was completed.

  - `created_at?: string`

    The unix timestamp of when the job was created.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `job_type?: JobType`

    The type of the job.

    - `"job"`

    - `"run"`

    - `"batch"`

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    The metadata of the job.

  - `status?: JobStatus`

    The status of the job.

    - `"created"`

    - `"running"`

    - `"completed"`

    - `"failed"`

    - `"pending"`

    - `"cancelled"`

    - `"expired"`

  - `stop_reason?: StopReasonType | null`

    The reason why the job was stopped.

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

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

### Stop Reason Type

- `StopReasonType = "end_turn" | "error" | "llm_api_error" | 10 more`

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

# Messages

## List Messages For Run

`client.runs.messages.list(stringrunID, MessageListParamsquery?, RequestOptionsoptions?): ArrayPage<Message>`

**get** `/v1/runs/{run_id}/messages`

Get response messages associated with a run.

### Parameters

- `runID: string`

- `query: MessageListParams`

  - `after?: string | null`

    Cursor for pagination (message ID). Returns results relative to this ID in the specified sort order. Expected format: 'message-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (message ID). Returns results relative to this ID in the specified sort order. Expected format: 'message-<uuid4>'

  - `limit?: number | null`

    Maximum number of messages to return

  - `order?: "asc" | "desc"`

    Sort order for messages by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `Message = SystemMessage | UserMessage | ReasoningMessage | 8 more`

  A message generated by the system. Never streamed back on a response, only used for cursor pagination.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  content (str): The message content sent by the system

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

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const message of client.runs.messages.list('run_id')) {
  console.log(message);
}
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

## Retrieve Stream For Run

`client.runs.messages.stream(stringrunID, MessageStreamParamsbody?, RequestOptionsoptions?): MessageStreamResponse | Stream<LettaStreamingResponse>`

**post** `/v1/runs/{run_id}/stream`

Retrieve Stream For Run

### Parameters

- `runID: string`

- `body: MessageStreamParams`

  - `agent_id?: string | null`

    Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

  - `batch_size?: number | null`

    Number of entries to read per batch.

  - `include_pings?: boolean | null`

    Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

  - `otid?: string | null`

    Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

  - `poll_interval?: number | null`

    Seconds to wait between polls when no new data.

  - `run_id?: string | null`

    Run ID to stream directly, bypassing run lookup. Use for recovery from duplicate requests.

  - `starting_after?: number`

    Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Returns

- `MessageStreamResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.runs.messages.stream('run_id');

console.log(response);
```

#### Response

```json
{}
```

## Domain Types

### Message Stream Response

- `MessageStreamResponse = unknown`

# Usage

## Retrieve Usage For Run

`client.runs.usage.retrieve(stringrunID, RequestOptionsoptions?): UsageRetrieveResponse`

**get** `/v1/runs/{run_id}/usage`

Get usage statistics for a run.

### Parameters

- `runID: string`

### Returns

- `UsageRetrieveResponse`

  - `completion_tokens?: number`

  - `completion_tokens_details?: CompletionTokensDetails | null`

    - `reasoning_tokens?: number | null`

  - `prompt_tokens?: number`

  - `prompt_tokens_details?: PromptTokensDetails | null`

    - `cache_creation_tokens?: number | null`

    - `cache_read_tokens?: number | null`

    - `cached_tokens?: number | null`

  - `total_tokens?: number`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const usage = await client.runs.usage.retrieve('run_id');

console.log(usage.completion_tokens);
```

#### Response

```json
{
  "completion_tokens": 0,
  "completion_tokens_details": {
    "reasoning_tokens": 0
  },
  "prompt_tokens": 0,
  "prompt_tokens_details": {
    "cache_creation_tokens": 0,
    "cache_read_tokens": 0,
    "cached_tokens": 0
  },
  "total_tokens": 0
}
```

## Domain Types

### Usage Retrieve Response

- `UsageRetrieveResponse`

  - `completion_tokens?: number`

  - `completion_tokens_details?: CompletionTokensDetails | null`

    - `reasoning_tokens?: number | null`

  - `prompt_tokens?: number`

  - `prompt_tokens_details?: PromptTokensDetails | null`

    - `cache_creation_tokens?: number | null`

    - `cache_read_tokens?: number | null`

    - `cached_tokens?: number | null`

  - `total_tokens?: number`

# Steps

## List Steps For Run

`client.runs.steps.list(stringrunID, StepListParamsquery?, RequestOptionsoptions?): ArrayPage<Step>`

**get** `/v1/runs/{run_id}/steps`

Get steps associated with a run with filtering options.

### Parameters

- `runID: string`

- `query: StepListParams`

  - `after?: string | null`

    Cursor for pagination (step ID). Returns results relative to this ID in the specified sort order. Expected format: 'step-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (step ID). Returns results relative to this ID in the specified sort order. Expected format: 'step-<uuid4>'

  - `limit?: number | null`

    Maximum number of messages to return

  - `order?: "asc" | "desc"`

    Sort order for steps by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `Step`

  - `id: string`

    The id of the step. Assigned by the database.

  - `agent_id?: string | null`

    The ID of the agent that performed the step.

  - `cache_write_tokens?: number | null`

    The number of input tokens written to cache (Anthropic only). None if not reported by provider.

  - `cached_input_tokens?: number | null`

    The number of input tokens served from cache. None if not reported by provider.

  - `completion_tokens?: number | null`

    The number of tokens generated by the agent during this step.

  - `completion_tokens_details?: Record<string, unknown> | null`

    Detailed completion token breakdown (e.g., reasoning_tokens).

  - `context_window_limit?: number | null`

    The context window limit configured for this step.

  - `error_data?: Record<string, unknown> | null`

    Error details including message, traceback, and additional context

  - `error_type?: string | null`

    The type/class of the error that occurred

  - `feedback?: "positive" | "negative" | null`

    The feedback for this step. Must be either 'positive' or 'negative'.

    - `"positive"`

    - `"negative"`

  - `messages?: Array<InternalMessage>`

    The messages generated during this step. Deprecated: use `GET /v1/steps/{step_id}/messages` endpoint instead

    - `id: string`

      The human-friendly ID of the Message

    - `role: MessageRole`

      The role of the participant.

      - `"assistant"`

      - `"user"`

      - `"tool"`

      - `"function"`

      - `"system"`

      - `"approval"`

      - `"summary"`

    - `agent_id?: string | null`

      The unique identifier of the agent.

    - `approval_request_id?: string | null`

      The id of the approval request if this message is associated with a tool call request.

    - `approvals?: Array<ApprovalReturn | LettaSchemasMessageToolReturnOutput> | null`

      The list of approvals for this message.

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

      - `LettaSchemasMessageToolReturnOutput`

        - `status: "success" | "error"`

          The status of the tool call

          - `"success"`

          - `"error"`

        - `func_response?: string | Array<TextContent | ImageContent> | null`

          The function response - either a string or list of content parts (text/image)

          - `string`

          - `Array<TextContent | ImageContent>`

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

        - `stderr?: Array<string> | null`

          Captured stderr from the tool invocation

        - `stdout?: Array<string> | null`

          Captured stdout (e.g. prints, logs) from the tool invocation

        - `tool_call_id?: unknown`

          The ID for the tool call

    - `approve?: boolean | null`

      Whether tool call is approved.

    - `batch_item_id?: string | null`

      The id of the LLMBatchItem that this message is associated with

    - `content?: Array<TextContent | ImageContent | ToolCallContent | 5 more> | null`

      The content of the message.

      - `TextContent`

      - `ImageContent`

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

    - `conversation_id?: string | null`

      The conversation this message belongs to

    - `created_at?: string`

      The timestamp when the object was created.

    - `created_by_id?: string | null`

      The id of the user that made this object.

    - `denial_reason?: string | null`

      The reason the tool call request was denied.

    - `group_id?: string | null`

      The multi-agent group that the message was sent in

    - `is_err?: boolean | null`

      Whether this message is part of an error step. Used only for debugging purposes.

    - `last_updated_by_id?: string | null`

      The id of the user that made this object.

    - `model?: string | null`

      The model used to make the function call.

    - `name?: string | null`

      For role user/assistant: the (optional) name of the participant. For role tool/function: the name of the function called.

    - `otid?: string | null`

      The offline threading id associated with this message

    - `run_id?: string | null`

      The id of the run that this message was created in.

    - `sender_id?: string | null`

      The id of the sender of the message, can be an identity id or agent id

    - `step_id?: string | null`

      The id of the step that this message was created in.

    - `tool_call_id?: string | null`

      The ID of the tool call. Only applicable for role tool.

    - `tool_calls?: Array<ToolCall> | null`

      The list of tool calls requested. Only applicable for role assistant.

      - `id: string`

      - `function: Function`

        The function that the model called.

        - `arguments: string`

        - `name: string`

      - `type: "function"`

        - `"function"`

    - `tool_returns?: Array<ToolReturn> | null`

      Tool execution return information for prior tool calls

      - `status: "success" | "error"`

        The status of the tool call

        - `"success"`

        - `"error"`

      - `func_response?: string | Array<TextContent | ImageContent> | null`

        The function response - either a string or list of content parts (text/image)

        - `string`

        - `Array<TextContent | ImageContent>`

          - `TextContent`

          - `ImageContent`

      - `stderr?: Array<string> | null`

        Captured stderr from the tool invocation

      - `stdout?: Array<string> | null`

        Captured stdout (e.g. prints, logs) from the tool invocation

      - `tool_call_id?: unknown`

        The ID for the tool call

    - `updated_at?: string | null`

      The timestamp when the object was last updated.

  - `model?: string | null`

    The name of the model used for this step.

  - `model_endpoint?: string | null`

    The model endpoint url used for this step.

  - `model_handle?: string | null`

    The model handle (e.g., 'openai/gpt-4o-mini') used for this step.

  - `origin?: string | null`

    The surface that this agent step was initiated from.

  - `project_id?: string | null`

    The project that the agent that executed this step belongs to (cloud only).

  - `prompt_tokens?: number | null`

    The number of tokens in the prompt during this step.

  - `prompt_tokens_details?: Record<string, unknown> | null`

    Detailed prompt token breakdown (e.g., cached_tokens, cache_read_tokens, cache_creation_tokens).

  - `provider_category?: string | null`

    The category of the provider used for this step.

  - `provider_id?: string | null`

    The unique identifier of the provider that was configured for this step

  - `provider_name?: string | null`

    The name of the provider used for this step.

  - `reasoning_tokens?: number | null`

    The number of reasoning/thinking tokens generated. None if not reported by provider.

  - `request_id?: string | null`

    The API request log ID from cloud-api for correlating steps with API requests.

  - `run_id?: string | null`

    The unique identifier of the run that this step belongs to. Only included for async calls.

  - `status?: "pending" | "success" | "failed" | "cancelled" | null`

    Status of a step execution

    - `"pending"`

    - `"success"`

    - `"failed"`

    - `"cancelled"`

  - `stop_reason?: StopReasonType | null`

    The stop reason associated with the step.

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

  - `tags?: Array<string>`

    Metadata tags.

  - `tid?: string | null`

    The unique identifier of the transaction that processed this step.

  - `total_tokens?: number | null`

    The total number of tokens processed by the agent during this step.

  - `trace_id?: string | null`

    The trace id of the agent step.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const step of client.runs.steps.list('run_id')) {
  console.log(step.id);
}
```

#### Response

```json
[
  {
    "id": "id",
    "agent_id": "agent_id",
    "cache_write_tokens": 0,
    "cached_input_tokens": 0,
    "completion_tokens": 0,
    "completion_tokens_details": {
      "foo": "bar"
    },
    "context_window_limit": 0,
    "error_data": {
      "foo": "bar"
    },
    "error_type": "error_type",
    "feedback": "positive",
    "messages": [
      {
        "id": "message-123e4567-e89b-12d3-a456-426614174000",
        "role": "assistant",
        "agent_id": "agent_id",
        "approval_request_id": "approval_request_id",
        "approvals": [
          {
            "approve": true,
            "tool_call_id": "tool_call_id",
            "reason": "reason",
            "type": "approval"
          }
        ],
        "approve": true,
        "batch_item_id": "batch_item_id",
        "content": [
          {
            "text": "text",
            "signature": "signature",
            "type": "text"
          }
        ],
        "conversation_id": "conversation_id",
        "created_at": "2019-12-27T18:11:19.117Z",
        "created_by_id": "created_by_id",
        "denial_reason": "denial_reason",
        "group_id": "group_id",
        "is_err": true,
        "last_updated_by_id": "last_updated_by_id",
        "model": "model",
        "name": "name",
        "otid": "otid",
        "run_id": "run_id",
        "sender_id": "sender_id",
        "step_id": "step_id",
        "tool_call_id": "tool_call_id",
        "tool_calls": [
          {
            "id": "id",
            "function": {
              "arguments": "arguments",
              "name": "name"
            },
            "type": "function"
          }
        ],
        "tool_returns": [
          {
            "status": "success",
            "func_response": "string",
            "stderr": [
              "string"
            ],
            "stdout": [
              "string"
            ],
            "tool_call_id": {}
          }
        ],
        "updated_at": "2019-12-27T18:11:19.117Z"
      }
    ],
    "model": "model",
    "model_endpoint": "model_endpoint",
    "model_handle": "model_handle",
    "origin": "origin",
    "project_id": "project_id",
    "prompt_tokens": 0,
    "prompt_tokens_details": {
      "foo": "bar"
    },
    "provider_category": "provider_category",
    "provider_id": "provider_id",
    "provider_name": "provider_name",
    "reasoning_tokens": 0,
    "request_id": "request_id",
    "run_id": "run_id",
    "status": "pending",
    "stop_reason": "end_turn",
    "tags": [
      "string"
    ],
    "tid": "tid",
    "total_tokens": 0,
    "trace_id": "trace_id"
  }
]
```

# Trace

## Retrieve Trace For Run

`client.runs.trace.retrieve(stringrunID, TraceRetrieveParamsquery?, RequestOptionsoptions?): TraceRetrieveResponse`

**get** `/v1/runs/{run_id}/trace`

Retrieve OTEL trace spans for a run.

Returns a filtered set of spans relevant for observability:

- agent_step: Individual agent reasoning steps
- tool executions: Tool call spans
- Root span: The top-level request span
- time_to_first_token: TTFT measurement span

Requires ClickHouse to be configured for trace storage.

### Parameters

- `runID: string`

- `query: TraceRetrieveParams`

  - `limit?: number`

    Maximum number of spans to return

### Returns

- `TraceRetrieveResponse = Array<Record<string, unknown>>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const traces = await client.runs.trace.retrieve('run_id');

console.log(traces);
```

#### Response

```json
[
  {
    "foo": "bar"
  }
]
```

## Domain Types

### Trace Retrieve Response

- `TraceRetrieveResponse = Array<Record<string, unknown>>`
