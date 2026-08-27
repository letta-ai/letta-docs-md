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
