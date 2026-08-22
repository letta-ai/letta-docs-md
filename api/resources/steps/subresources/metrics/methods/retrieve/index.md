## Retrieve Metrics For Step

**get** `/v1/steps/{step_id}/metrics`

Get step metrics by step ID.

### Path Parameters

- `step_id: string`

  The ID of the step in the format 'step-<uuid4>'

### Returns

- `id: string`

  The id of the step this metric belongs to (matches steps.id).

- `agent_id: optional string`

  The unique identifier of the agent.

- `base_template_id: optional string`

  The base template ID that the step belongs to (cloud only).

- `llm_request_ns: optional number`

  Time spent on LLM requests in nanoseconds.

- `llm_request_start_ns: optional number`

  The timestamp of the start of the llm request in nanoseconds.

- `project_id: optional string`

  The project that the step belongs to (cloud only).

- `provider_id: optional string`

  The unique identifier of the provider.

- `run_id: optional string`

  The unique identifier of the run.

- `step_ns: optional number`

  Total time for the step in nanoseconds.

- `step_start_ns: optional number`

  The timestamp of the start of the step in nanoseconds.

- `template_id: optional string`

  The template ID that the step belongs to (cloud only).

- `tool_execution_ns: optional number`

  Time spent on tool execution in nanoseconds.

### Example

```http
curl https://api.letta.com/v1/steps/$STEP_ID/metrics \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "id": "id",
  "agent_id": "agent_id",
  "base_template_id": "base_template_id",
  "llm_request_ns": 0,
  "llm_request_start_ns": 0,
  "project_id": "project_id",
  "provider_id": "provider_id",
  "run_id": "run_id",
  "step_ns": 0,
  "step_start_ns": 0,
  "template_id": "template_id",
  "tool_execution_ns": 0
}
```
