## List Runs

**get** `/v1/runs/`

List all runs.

### Query Parameters

- `active: optional boolean`

  Filter for active runs.

- `after: optional string`

  Cursor for pagination (run ID). Returns results relative to this ID in the specified sort order. Expected format: 'run-<uuid4>'

- `agent_id: optional string`

  The unique identifier of the agent associated with the run.

- `agent_ids: optional array of string`

  The unique identifiers of the agents associated with the run. Deprecated in favor of agent_id field.

- `ascending: optional boolean`

  Whether to sort agents oldest to newest (True) or newest to oldest (False, default). Deprecated in favor of order field.

- `background: optional boolean`

  If True, filters for runs that were created in background mode.

- `before: optional string`

  Cursor for pagination (run ID). Returns results relative to this ID in the specified sort order. Expected format: 'run-<uuid4>'

- `conversation_id: optional string`

  Filter runs by conversation ID.

- `limit: optional number`

  Maximum number of runs to return

- `order: optional "asc" or "desc"`

  Sort order for runs by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

- `statuses: optional array of string`

  Filter runs by status. Can specify multiple statuses.

- `stop_reason: optional StopReasonType`

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
curl https://api.letta.com/v1/runs/ \
    -H "Authorization: Bearer $LETTA_API_KEY"
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
