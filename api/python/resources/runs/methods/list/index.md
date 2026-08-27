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
