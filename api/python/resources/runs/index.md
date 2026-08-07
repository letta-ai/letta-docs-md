# Runs

## List Runs

`runs.list(RunListParams**kwargs)  -> SyncArrayPage[Run]`

**get** `/v1/runs/`

List all runs.

### Parameters

- `active: Optional[bool]`

  Filter for active runs.

- `after: Optional[str]`

  Cursor for pagination (run ID). Returns results relative to this ID in the specified sort order. Expected format: 'run-<uuid4>'

- `agent_id: Optional[str]`

  The unique identifier of the agent associated with the run.

- `agent_ids: Optional[Sequence[str]]`

  The unique identifiers of the agents associated with the run. Deprecated in favor of agent_id field.

- `ascending: Optional[bool]`

  Whether to sort agents oldest to newest (True) or newest to oldest (False, default). Deprecated in favor of order field.

- `background: Optional[bool]`

  If True, filters for runs that were created in background mode.

- `before: Optional[str]`

  Cursor for pagination (run ID). Returns results relative to this ID in the specified sort order. Expected format: 'run-<uuid4>'

- `conversation_id: Optional[str]`

  Filter runs by conversation ID.

- `limit: Optional[int]`

  Maximum number of runs to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for runs by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

- `statuses: Optional[Sequence[str]]`

  Filter runs by status. Can specify multiple statuses.

- `stop_reason: Optional[StopReasonType]`

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

- `class Run: …`

  Representation of a run - a conversation or processing session for an agent. Runs track when agents process messages and maintain the relationship between agents, steps, and messages.

  - `id: str`

    The human-friendly ID of the Run

  - `agent_id: str`

    The unique identifier of the agent associated with the run.

  - `background: Optional[bool]`

    Whether the run was created in background mode.

  - `base_template_id: Optional[str]`

    The base template ID that the run belongs to.

  - `callback_error: Optional[str]`

    Optional error message from attempting to POST the callback endpoint.

  - `callback_sent_at: Optional[datetime]`

    Timestamp when the callback was last attempted.

  - `callback_status_code: Optional[int]`

    HTTP status code returned by the callback endpoint.

  - `callback_url: Optional[str]`

    If set, POST to this URL when the run completes.

  - `completed_at: Optional[datetime]`

    The timestamp when the run was completed.

  - `conversation_id: Optional[str]`

    The unique identifier of the conversation associated with the run.

  - `created_at: Optional[datetime]`

    The timestamp when the run was created.

  - `metadata: Optional[Dict[str, object]]`

    Additional metadata for the run.

  - `request_config: Optional[RequestConfig]`

    The request configuration for the run.

    - `assistant_message_tool_kwarg: Optional[str]`

      The name of the message argument in the designated message tool.

    - `assistant_message_tool_name: Optional[str]`

      The name of the designated message tool.

    - `include_return_message_types: Optional[List[MessageType]]`

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

    - `use_assistant_message: Optional[bool]`

      Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects.

  - `status: Optional[Literal["created", "running", "completed", 2 more]]`

    The current status of the run.

    - `"created"`

    - `"running"`

    - `"completed"`

    - `"failed"`

    - `"cancelled"`

  - `stop_reason: Optional[StopReasonType]`

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

  - `total_duration_ns: Optional[int]`

    Total run duration in nanoseconds

  - `ttft_ns: Optional[int]`

    Time to first token for a run in nanoseconds

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.runs.list()
page = page.items[0]
print(page.id)
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

`runs.retrieve(strrun_id)  -> Run`

**get** `/v1/runs/{run_id}`

Get the status of a run.

### Parameters

- `run_id: str`

### Returns

- `class Run: …`

  Representation of a run - a conversation or processing session for an agent. Runs track when agents process messages and maintain the relationship between agents, steps, and messages.

  - `id: str`

    The human-friendly ID of the Run

  - `agent_id: str`

    The unique identifier of the agent associated with the run.

  - `background: Optional[bool]`

    Whether the run was created in background mode.

  - `base_template_id: Optional[str]`

    The base template ID that the run belongs to.

  - `callback_error: Optional[str]`

    Optional error message from attempting to POST the callback endpoint.

  - `callback_sent_at: Optional[datetime]`

    Timestamp when the callback was last attempted.

  - `callback_status_code: Optional[int]`

    HTTP status code returned by the callback endpoint.

  - `callback_url: Optional[str]`

    If set, POST to this URL when the run completes.

  - `completed_at: Optional[datetime]`

    The timestamp when the run was completed.

  - `conversation_id: Optional[str]`

    The unique identifier of the conversation associated with the run.

  - `created_at: Optional[datetime]`

    The timestamp when the run was created.

  - `metadata: Optional[Dict[str, object]]`

    Additional metadata for the run.

  - `request_config: Optional[RequestConfig]`

    The request configuration for the run.

    - `assistant_message_tool_kwarg: Optional[str]`

      The name of the message argument in the designated message tool.

    - `assistant_message_tool_name: Optional[str]`

      The name of the designated message tool.

    - `include_return_message_types: Optional[List[MessageType]]`

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

    - `use_assistant_message: Optional[bool]`

      Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects.

  - `status: Optional[Literal["created", "running", "completed", 2 more]]`

    The current status of the run.

    - `"created"`

    - `"running"`

    - `"completed"`

    - `"failed"`

    - `"cancelled"`

  - `stop_reason: Optional[StopReasonType]`

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

  - `total_duration_ns: Optional[int]`

    Total run duration in nanoseconds

  - `ttft_ns: Optional[int]`

    Time to first token for a run in nanoseconds

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
run = client.runs.retrieve(
    "run_id",
)
print(run.id)
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

- `class Job: …`

  Representation of offline jobs, used for tracking status of data loading tasks (involving parsing and embedding files).

  - `id: Optional[str]`

    The human-friendly ID of the Job

  - `agent_id: Optional[str]`

    The agent associated with this job/run.

  - `background: Optional[bool]`

    Whether the job was created in background mode.

  - `callback_error: Optional[str]`

    Optional error message from attempting to POST the callback endpoint.

  - `callback_sent_at: Optional[datetime]`

    Timestamp when the callback was last attempted.

  - `callback_status_code: Optional[int]`

    HTTP status code returned by the callback endpoint.

  - `callback_url: Optional[str]`

    If set, POST to this URL when the job completes.

  - `completed_at: Optional[datetime]`

    The unix timestamp of when the job was completed.

  - `created_at: Optional[datetime]`

    The unix timestamp of when the job was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `job_type: Optional[JobType]`

    The type of the job.

    - `"job"`

    - `"run"`

    - `"batch"`

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `metadata: Optional[Dict[str, object]]`

    The metadata of the job.

  - `status: Optional[JobStatus]`

    The status of the job.

    - `"created"`

    - `"running"`

    - `"completed"`

    - `"failed"`

    - `"pending"`

    - `"cancelled"`

    - `"expired"`

  - `stop_reason: Optional[StopReasonType]`

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

  - `total_duration_ns: Optional[int]`

    Total run duration in nanoseconds

  - `ttft_ns: Optional[int]`

    Time to first token for a run in nanoseconds

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

### Stop Reason Type

- `Literal["end_turn", "error", "llm_api_error", 10 more]`

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

`runs.messages.list(strrun_id, MessageListParams**kwargs)  -> SyncArrayPage[Message]`

**get** `/v1/runs/{run_id}/messages`

Get response messages associated with a run.

### Parameters

- `run_id: str`

- `after: Optional[str]`

  Cursor for pagination (message ID). Returns results relative to this ID in the specified sort order. Expected format: 'message-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (message ID). Returns results relative to this ID in the specified sort order. Expected format: 'message-<uuid4>'

- `limit: Optional[int]`

  Maximum number of messages to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for messages by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `Message`

  A message generated by the system. Never streamed back on a response, only used for cursor pagination.

  Args:
  id (str): The ID of the message
  date (datetime): The date the message was created in ISO format
  name (Optional[str]): The name of the sender of the message
  content (str): The message content sent by the system

  - `class SystemMessage: …`

    A message generated by the system. Never streamed back on a response, only used for cursor pagination.

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    content (str): The message content sent by the system

    - `id: str`

    - `content: str`

      The message content sent by the system

    - `date: datetime`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["system_message"]]`

      The type of the message.

      - `"system_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

  - `class UserMessage: …`

    A message sent by the user. Never streamed back on a response, only used for cursor pagination.

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    content (Union[str, List[LettaUserMessageContentUnion]]): The message content sent by the user (can be a string or an array of multi-modal content parts)

    - `id: str`

    - `content: Union[List[LettaUserMessageContentUnion], str]`

      The message content sent by the user (can be a string or an array of multi-modal content parts)

      - `List[LettaUserMessageContentUnion]`

        - `class TextContent: …`

          - `text: str`

            The text content of the message.

          - `signature: Optional[str]`

            Stores a unique identifier for any reasoning associated with this text content.

          - `type: Optional[Literal["text"]]`

            The type of the message.

            - `"text"`

        - `class ImageContent: …`

          - `source: Source`

            The source of the image.

            - `class SourceURLImage: …`

              - `url: str`

                The URL of the image.

              - `type: Optional[Literal["url"]]`

                The source type for the image.

                - `"url"`

            - `class SourceBase64Image: …`

              - `data: str`

                The base64 encoded image data.

              - `media_type: str`

                The media type for the image.

              - `detail: Optional[str]`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `type: Optional[Literal["base64"]]`

                The source type for the image.

                - `"base64"`

            - `class SourceLettaImage: …`

              - `file_id: str`

                The unique identifier of the image file persisted in storage.

              - `data: Optional[str]`

                The base64 encoded image data.

              - `detail: Optional[str]`

                What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

              - `media_type: Optional[str]`

                The media type for the image.

              - `type: Optional[Literal["letta"]]`

                The source type for the image.

                - `"letta"`

          - `type: Optional[Literal["image"]]`

            The type of the message.

            - `"image"`

      - `str`

    - `date: datetime`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["user_message"]]`

      The type of the message.

      - `"user_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

  - `class ReasoningMessage: …`

    Representation of an agent's internal reasoning.

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    source (Literal["reasoner_model", "non_reasoner_model"]): Whether the reasoning
    content was generated natively by a reasoner model or derived via prompting
    reasoning (str): The internal reasoning of the agent
    signature (Optional[str]): The model-generated signature of the reasoning step

    - `id: str`

    - `date: datetime`

    - `reasoning: str`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["reasoning_message"]]`

      The type of the message.

      - `"reasoning_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `signature: Optional[str]`

    - `source: Optional[Literal["reasoner_model", "non_reasoner_model"]]`

      - `"reasoner_model"`

      - `"non_reasoner_model"`

    - `step_id: Optional[str]`

  - `class HiddenReasoningMessage: …`

    Representation of an agent's internal reasoning where reasoning content
    has been hidden from the response.

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    state (Literal["redacted", "omitted"]): Whether the reasoning
    content was redacted by the provider or simply omitted by the API
    hidden_reasoning (Optional[str]): The internal reasoning of the agent

    - `id: str`

    - `date: datetime`

    - `state: Literal["redacted", "omitted"]`

      - `"redacted"`

      - `"omitted"`

    - `hidden_reasoning: Optional[str]`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["hidden_reasoning_message"]]`

      The type of the message.

      - `"hidden_reasoning_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

  - `class ToolCallMessage: …`

    A message representing a request to call a tool (generated by the LLM to trigger tool execution).

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    tool_call (Union[ToolCall, ToolCallDelta]): The tool call

    - `id: str`

    - `date: datetime`

    - `tool_call: ToolCall`

      - `class ToolCall: …`

        - `arguments: str`

        - `name: str`

        - `tool_call_id: str`

      - `class ToolCallDelta: …`

        - `arguments: Optional[str]`

        - `name: Optional[str]`

        - `tool_call_id: Optional[str]`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["tool_call_message"]]`

      The type of the message.

      - `"tool_call_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

    - `tool_calls: Optional[ToolCalls]`

      - `List[ToolCall]`

        - `arguments: str`

        - `name: str`

        - `tool_call_id: str`

      - `class ToolCallDelta: …`

  - `class ToolReturnMessage: …`

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

    - `id: str`

    - `date: datetime`

    - `status: Literal["success", "error"]`

      - `"success"`

      - `"error"`

    - `tool_call_id: str`

    - `tool_return: str`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["tool_return_message"]]`

      The type of the message.

      - `"tool_return_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `stderr: Optional[List[str]]`

    - `stdout: Optional[List[str]]`

    - `step_id: Optional[str]`

    - `tool_returns: Optional[List[ToolReturn]]`

      - `status: Literal["success", "error"]`

        - `"success"`

        - `"error"`

      - `tool_call_id: str`

      - `tool_return: Union[List[ToolReturnUnionMember0], str]`

        The tool return value - either a string or list of content parts (text/image)

        - `List[ToolReturnUnionMember0]`

          - `class TextContent: …`

          - `class ImageContent: …`

        - `str`

      - `stderr: Optional[List[str]]`

      - `stdout: Optional[List[str]]`

      - `type: Optional[Literal["tool"]]`

        The message type to be created.

        - `"tool"`

  - `class AssistantMessage: …`

    A message sent by the LLM in response to user input. Used in the LLM context.

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    content (Union[str, List[LettaAssistantMessageContentUnion]]): The message content sent by the agent (can be a string or an array of content parts)

    - `id: str`

    - `content: Union[List[LettaAssistantMessageContentUnion], str]`

      The message content sent by the agent (can be a string or an array of content parts)

      - `List[LettaAssistantMessageContentUnion]`

        - `text: str`

          The text content of the message.

        - `signature: Optional[str]`

          Stores a unique identifier for any reasoning associated with this text content.

        - `type: Optional[Literal["text"]]`

          The type of the message.

          - `"text"`

      - `str`

    - `date: datetime`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["assistant_message"]]`

      The type of the message.

      - `"assistant_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

  - `class ApprovalRequestMessage: …`

    A message representing a request for approval to call a tool (generated by the LLM to trigger tool execution).

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    tool_call (ToolCall): The tool call

    - `id: str`

    - `date: datetime`

    - `tool_call: ToolCall`

      The tool call that has been requested by the llm to run

      - `class ToolCall: …`

      - `class ToolCallDelta: …`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["approval_request_message"]]`

      The type of the message.

      - `"approval_request_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

    - `tool_calls: Optional[ToolCalls]`

      The tool calls that have been requested by the llm to run, which are pending approval

      - `List[ToolCall]`

        - `arguments: str`

        - `name: str`

        - `tool_call_id: str`

      - `class ToolCallDelta: …`

  - `class ApprovalResponseMessage: …`

    A message representing a response form the user indicating whether a tool has been approved to run.

    Args:
    id (str): The ID of the message
    date (datetime): The date the message was created in ISO format
    name (Optional[str]): The name of the sender of the message
    approve: (bool) Whether the tool has been approved
    approval_request_id: The ID of the approval request
    reason: (Optional[str]) An optional explanation for the provided approval status

    - `id: str`

    - `date: datetime`

    - `approval_request_id: Optional[str]`

      The message ID of the approval request

    - `approvals: Optional[List[Approval]]`

      The list of approval responses

      - `class ApprovalReturn: …`

        - `approve: bool`

          Whether the tool has been approved

        - `tool_call_id: str`

          The ID of the tool call that corresponds to this approval

        - `reason: Optional[str]`

          An optional explanation for the provided approval status

        - `type: Optional[Literal["approval"]]`

          The message type to be created.

          - `"approval"`

      - `class ToolReturn: …`

        - `status: Literal["success", "error"]`

        - `tool_call_id: str`

        - `tool_return: Union[List[ToolReturnUnionMember0], str]`

          The tool return value - either a string or list of content parts (text/image)

        - `stderr: Optional[List[str]]`

        - `stdout: Optional[List[str]]`

        - `type: Optional[Literal["tool"]]`

          The message type to be created.

    - `approve: Optional[bool]`

      Whether the tool has been approved

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["approval_response_message"]]`

      The type of the message.

      - `"approval_response_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `reason: Optional[str]`

      An optional explanation for the provided approval status

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

  - `class SummaryMessage: …`

    A message representing a summary of the conversation. Sent to the LLM as a user or system message depending on the provider.

    - `id: str`

    - `date: datetime`

    - `summary: str`

    - `compaction_stats: Optional[CompactionStats]`

      Statistics about a memory compaction operation.

      - `context_window: int`

        The model's context window size

      - `messages_count_after: int`

        Number of messages after compaction

      - `messages_count_before: int`

        Number of messages before compaction

      - `trigger: str`

        What triggered the compaction (e.g., 'context_window_exceeded', 'post_step_context_check')

      - `context_tokens_after: Optional[int]`

        Token count after compaction (message tokens only, does not include tool definitions)

      - `context_tokens_before: Optional[int]`

        Token count before compaction (from LLM usage stats, includes full context sent to LLM)

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["summary_message"]]`

      - `"summary_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

  - `class EventMessage: …`

    A message for notifying the developer that an event that has occured (e.g. a compaction). Events are NOT part of the context window.

    - `id: str`

    - `date: datetime`

    - `event_data: Dict[str, object]`

    - `event_type: Literal["compaction"]`

      - `"compaction"`

    - `is_err: Optional[bool]`

    - `message_type: Optional[Literal["event_message"]]`

      - `"event_message"`

    - `name: Optional[str]`

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `run_id: Optional[str]`

    - `sender_id: Optional[str]`

    - `seq_id: Optional[int]`

    - `step_id: Optional[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.runs.messages.list(
    run_id="run_id",
)
page = page.items[0]
print(page)
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

`runs.messages.stream(strpath_run_id, MessageStreamParams**kwargs)  -> object`

**post** `/v1/runs/{run_id}/stream`

Retrieve Stream For Run

### Parameters

- `run_id: str`

- `agent_id: Optional[str]`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `batch_size: Optional[int]`

  Number of entries to read per batch.

- `include_pings: Optional[bool]`

  Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

- `otid: Optional[str]`

  Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

- `poll_interval: Optional[float]`

  Seconds to wait between polls when no new data.

- `run_id: str`

- `starting_after: Optional[int]`

  Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
for message in client.runs.messages.stream(
    path_run_id="run_id",
):
  print(message)
```

#### Response

```json
{}
```

# Usage

## Retrieve Usage For Run

`runs.usage.retrieve(strrun_id)  -> UsageRetrieveResponse`

**get** `/v1/runs/{run_id}/usage`

Get usage statistics for a run.

### Parameters

- `run_id: str`

### Returns

- `class UsageRetrieveResponse: …`

  - `completion_tokens: Optional[int]`

  - `completion_tokens_details: Optional[CompletionTokensDetails]`

    - `reasoning_tokens: Optional[int]`

  - `prompt_tokens: Optional[int]`

  - `prompt_tokens_details: Optional[PromptTokensDetails]`

    - `cache_creation_tokens: Optional[int]`

    - `cache_read_tokens: Optional[int]`

    - `cached_tokens: Optional[int]`

  - `total_tokens: Optional[int]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
usage = client.runs.usage.retrieve(
    "run_id",
)
print(usage.completion_tokens)
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

- `class UsageRetrieveResponse: …`

  - `completion_tokens: Optional[int]`

  - `completion_tokens_details: Optional[CompletionTokensDetails]`

    - `reasoning_tokens: Optional[int]`

  - `prompt_tokens: Optional[int]`

  - `prompt_tokens_details: Optional[PromptTokensDetails]`

    - `cache_creation_tokens: Optional[int]`

    - `cache_read_tokens: Optional[int]`

    - `cached_tokens: Optional[int]`

  - `total_tokens: Optional[int]`

# Steps

## List Steps For Run

`runs.steps.list(strrun_id, StepListParams**kwargs)  -> SyncArrayPage[Step]`

**get** `/v1/runs/{run_id}/steps`

Get steps associated with a run with filtering options.

### Parameters

- `run_id: str`

- `after: Optional[str]`

  Cursor for pagination (step ID). Returns results relative to this ID in the specified sort order. Expected format: 'step-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (step ID). Returns results relative to this ID in the specified sort order. Expected format: 'step-<uuid4>'

- `limit: Optional[int]`

  Maximum number of messages to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for steps by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `class Step: …`

  - `id: str`

    The id of the step. Assigned by the database.

  - `agent_id: Optional[str]`

    The ID of the agent that performed the step.

  - `cache_write_tokens: Optional[int]`

    The number of input tokens written to cache (Anthropic only). None if not reported by provider.

  - `cached_input_tokens: Optional[int]`

    The number of input tokens served from cache. None if not reported by provider.

  - `completion_tokens: Optional[int]`

    The number of tokens generated by the agent during this step.

  - `completion_tokens_details: Optional[Dict[str, object]]`

    Detailed completion token breakdown (e.g., reasoning_tokens).

  - `context_window_limit: Optional[int]`

    The context window limit configured for this step.

  - `error_data: Optional[Dict[str, object]]`

    Error details including message, traceback, and additional context

  - `error_type: Optional[str]`

    The type/class of the error that occurred

  - `feedback: Optional[Literal["positive", "negative"]]`

    The feedback for this step. Must be either 'positive' or 'negative'.

    - `"positive"`

    - `"negative"`

  - `messages: Optional[List[InternalMessage]]`

    The messages generated during this step. Deprecated: use `GET /v1/steps/{step_id}/messages` endpoint instead

    - `id: str`

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

    - `agent_id: Optional[str]`

      The unique identifier of the agent.

    - `approval_request_id: Optional[str]`

      The id of the approval request if this message is associated with a tool call request.

    - `approvals: Optional[List[Approval]]`

      The list of approvals for this message.

      - `class ApprovalReturn: …`

        - `approve: bool`

          Whether the tool has been approved

        - `tool_call_id: str`

          The ID of the tool call that corresponds to this approval

        - `reason: Optional[str]`

          An optional explanation for the provided approval status

        - `type: Optional[Literal["approval"]]`

          The message type to be created.

          - `"approval"`

      - `class ApprovalLettaSchemasMessageToolReturnOutput: …`

        - `status: Literal["success", "error"]`

          The status of the tool call

          - `"success"`

          - `"error"`

        - `func_response: Optional[Union[str, List[ApprovalLettaSchemasMessageToolReturnOutputFuncResponseUnionMember1], null]]`

          The function response - either a string or list of content parts (text/image)

          - `str`

          - `List[ApprovalLettaSchemasMessageToolReturnOutputFuncResponseUnionMember1]`

            - `class TextContent: …`

              - `text: str`

                The text content of the message.

              - `signature: Optional[str]`

                Stores a unique identifier for any reasoning associated with this text content.

              - `type: Optional[Literal["text"]]`

                The type of the message.

                - `"text"`

            - `class ImageContent: …`

              - `source: Source`

                The source of the image.

                - `class SourceURLImage: …`

                  - `url: str`

                    The URL of the image.

                  - `type: Optional[Literal["url"]]`

                    The source type for the image.

                    - `"url"`

                - `class SourceBase64Image: …`

                  - `data: str`

                    The base64 encoded image data.

                  - `media_type: str`

                    The media type for the image.

                  - `detail: Optional[str]`

                    What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

                  - `type: Optional[Literal["base64"]]`

                    The source type for the image.

                    - `"base64"`

                - `class SourceLettaImage: …`

                  - `file_id: str`

                    The unique identifier of the image file persisted in storage.

                  - `data: Optional[str]`

                    The base64 encoded image data.

                  - `detail: Optional[str]`

                    What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

                  - `media_type: Optional[str]`

                    The media type for the image.

                  - `type: Optional[Literal["letta"]]`

                    The source type for the image.

                    - `"letta"`

              - `type: Optional[Literal["image"]]`

                The type of the message.

                - `"image"`

        - `stderr: Optional[List[str]]`

          Captured stderr from the tool invocation

        - `stdout: Optional[List[str]]`

          Captured stdout (e.g. prints, logs) from the tool invocation

        - `tool_call_id: Optional[object]`

          The ID for the tool call

    - `approve: Optional[bool]`

      Whether tool call is approved.

    - `batch_item_id: Optional[str]`

      The id of the LLMBatchItem that this message is associated with

    - `content: Optional[List[Content]]`

      The content of the message.

      - `class TextContent: …`

      - `class ImageContent: …`

      - `class ToolCallContent: …`

        - `id: str`

          A unique identifier for this specific tool call instance.

        - `input: Dict[str, object]`

          The parameters being passed to the tool, structured as a dictionary of parameter names to values.

        - `name: str`

          The name of the tool being called.

        - `signature: Optional[str]`

          Stores a unique identifier for any reasoning associated with this tool call.

        - `type: Optional[Literal["tool_call"]]`

          Indicates this content represents a tool call event.

          - `"tool_call"`

      - `class ToolReturnContent: …`

        - `content: str`

          The content returned by the tool execution.

        - `is_error: bool`

          Indicates whether the tool execution resulted in an error.

        - `tool_call_id: str`

          References the ID of the ToolCallContent that initiated this tool call.

        - `type: Optional[Literal["tool_return"]]`

          Indicates this content represents a tool return event.

          - `"tool_return"`

      - `class ReasoningContent: …`

        Sent via the Anthropic Messages API

        - `is_native: bool`

          Whether the reasoning content was generated by a reasoner model that processed this step.

        - `reasoning: str`

          The intermediate reasoning or thought process content.

        - `signature: Optional[str]`

          A unique identifier for this reasoning step.

        - `type: Optional[Literal["reasoning"]]`

          Indicates this is a reasoning/intermediate step.

          - `"reasoning"`

      - `class RedactedReasoningContent: …`

        Sent via the Anthropic Messages API

        - `data: str`

          The redacted or filtered intermediate reasoning content.

        - `type: Optional[Literal["redacted_reasoning"]]`

          Indicates this is a redacted thinking step.

          - `"redacted_reasoning"`

      - `class OmittedReasoningContent: …`

        A placeholder for reasoning content we know is present, but isn't returned by the provider (e.g. OpenAI GPT-5 on ChatCompletions)

        - `signature: Optional[str]`

          A unique identifier for this reasoning step.

        - `type: Optional[Literal["omitted_reasoning"]]`

          Indicates this is an omitted reasoning step.

          - `"omitted_reasoning"`

      - `class ContentSummarizedReasoningContent: …`

        The style of reasoning content returned by the OpenAI Responses API

        - `id: str`

          The unique identifier for this reasoning step.

        - `summary: List[ContentSummarizedReasoningContentSummary]`

          Summaries of the reasoning content.

          - `index: int`

            The index of the summary part.

          - `text: str`

            The text of the summary part.

        - `encrypted_content: Optional[str]`

          The encrypted reasoning content.

        - `type: Optional[Literal["summarized_reasoning"]]`

          Indicates this is a summarized reasoning step.

          - `"summarized_reasoning"`

    - `conversation_id: Optional[str]`

      The conversation this message belongs to

    - `created_at: Optional[datetime]`

      The timestamp when the object was created.

    - `created_by_id: Optional[str]`

      The id of the user that made this object.

    - `denial_reason: Optional[str]`

      The reason the tool call request was denied.

    - `group_id: Optional[str]`

      The multi-agent group that the message was sent in

    - `is_err: Optional[bool]`

      Whether this message is part of an error step. Used only for debugging purposes.

    - `last_updated_by_id: Optional[str]`

      The id of the user that made this object.

    - `model: Optional[str]`

      The model used to make the function call.

    - `name: Optional[str]`

      For role user/assistant: the (optional) name of the participant. For role tool/function: the name of the function called.

    - `otid: Optional[str]`

      The offline threading id associated with this message

    - `run_id: Optional[str]`

      The id of the run that this message was created in.

    - `sender_id: Optional[str]`

      The id of the sender of the message, can be an identity id or agent id

    - `step_id: Optional[str]`

      The id of the step that this message was created in.

    - `tool_call_id: Optional[str]`

      The ID of the tool call. Only applicable for role tool.

    - `tool_calls: Optional[List[ToolCall]]`

      The list of tool calls requested. Only applicable for role assistant.

      - `id: str`

      - `function: ToolCallFunction`

        The function that the model called.

        - `arguments: str`

        - `name: str`

      - `type: Literal["function"]`

        - `"function"`

    - `tool_returns: Optional[List[ToolReturn]]`

      Tool execution return information for prior tool calls

      - `status: Literal["success", "error"]`

        The status of the tool call

        - `"success"`

        - `"error"`

      - `func_response: Optional[Union[str, List[ToolReturnFuncResponseUnionMember1], null]]`

        The function response - either a string or list of content parts (text/image)

        - `str`

        - `List[ToolReturnFuncResponseUnionMember1]`

          - `class TextContent: …`

          - `class ImageContent: …`

      - `stderr: Optional[List[str]]`

        Captured stderr from the tool invocation

      - `stdout: Optional[List[str]]`

        Captured stdout (e.g. prints, logs) from the tool invocation

      - `tool_call_id: Optional[object]`

        The ID for the tool call

    - `updated_at: Optional[datetime]`

      The timestamp when the object was last updated.

  - `model: Optional[str]`

    The name of the model used for this step.

  - `model_endpoint: Optional[str]`

    The model endpoint url used for this step.

  - `model_handle: Optional[str]`

    The model handle (e.g., 'openai/gpt-4o-mini') used for this step.

  - `origin: Optional[str]`

    The surface that this agent step was initiated from.

  - `project_id: Optional[str]`

    The project that the agent that executed this step belongs to (cloud only).

  - `prompt_tokens: Optional[int]`

    The number of tokens in the prompt during this step.

  - `prompt_tokens_details: Optional[Dict[str, object]]`

    Detailed prompt token breakdown (e.g., cached_tokens, cache_read_tokens, cache_creation_tokens).

  - `provider_category: Optional[str]`

    The category of the provider used for this step.

  - `provider_id: Optional[str]`

    The unique identifier of the provider that was configured for this step

  - `provider_name: Optional[str]`

    The name of the provider used for this step.

  - `reasoning_tokens: Optional[int]`

    The number of reasoning/thinking tokens generated. None if not reported by provider.

  - `request_id: Optional[str]`

    The API request log ID from cloud-api for correlating steps with API requests.

  - `run_id: Optional[str]`

    The unique identifier of the run that this step belongs to. Only included for async calls.

  - `status: Optional[Literal["pending", "success", "failed", "cancelled"]]`

    Status of a step execution

    - `"pending"`

    - `"success"`

    - `"failed"`

    - `"cancelled"`

  - `stop_reason: Optional[StopReasonType]`

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

  - `tags: Optional[List[str]]`

    Metadata tags.

  - `tid: Optional[str]`

    The unique identifier of the transaction that processed this step.

  - `total_tokens: Optional[int]`

    The total number of tokens processed by the agent during this step.

  - `trace_id: Optional[str]`

    The trace id of the agent step.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.runs.steps.list(
    run_id="run_id",
)
page = page.items[0]
print(page.id)
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

`runs.trace.retrieve(strrun_id, TraceRetrieveParams**kwargs)  -> TraceRetrieveResponse`

**get** `/v1/runs/{run_id}/trace`

Retrieve OTEL trace spans for a run.

Returns a filtered set of spans relevant for observability:

- agent_step: Individual agent reasoning steps
- tool executions: Tool call spans
- Root span: The top-level request span
- time_to_first_token: TTFT measurement span

Requires ClickHouse to be configured for trace storage.

### Parameters

- `run_id: str`

- `limit: Optional[int]`

  Maximum number of spans to return

### Returns

- `List[Dict[str, object]]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
traces = client.runs.trace.retrieve(
    run_id="run_id",
)
print(traces)
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

- `List[Dict[str, object]]`
