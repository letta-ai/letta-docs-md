# Metrics

## Retrieve Metrics For Step

`client.steps.metrics.retrieve(stringstepID, RequestOptionsoptions?): MetricRetrieveResponse`

**get** `/v1/steps/{step_id}/metrics`

Get step metrics by step ID.

### Parameters

- `stepID: string`

  The ID of the step in the format 'step-<uuid4>'

### Returns

- `MetricRetrieveResponse`

  - `id: string`

    The id of the step this metric belongs to (matches steps.id).

  - `agent_id?: string | null`

    The unique identifier of the agent.

  - `base_template_id?: string | null`

    The base template ID that the step belongs to (cloud only).

  - `llm_request_ns?: number | null`

    Time spent on LLM requests in nanoseconds.

  - `llm_request_start_ns?: number | null`

    The timestamp of the start of the llm request in nanoseconds.

  - `project_id?: string | null`

    The project that the step belongs to (cloud only).

  - `provider_id?: string | null`

    The unique identifier of the provider.

  - `run_id?: string | null`

    The unique identifier of the run.

  - `step_ns?: number | null`

    Total time for the step in nanoseconds.

  - `step_start_ns?: number | null`

    The timestamp of the start of the step in nanoseconds.

  - `template_id?: string | null`

    The template ID that the step belongs to (cloud only).

  - `tool_execution_ns?: number | null`

    Time spent on tool execution in nanoseconds.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const metric = await client.steps.metrics.retrieve('step-123e4567-e89b-42d3-8456-426614174000');

console.log(metric.id);
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

## Domain Types

### Metric Retrieve Response

- `MetricRetrieveResponse`

  - `id: string`

    The id of the step this metric belongs to (matches steps.id).

  - `agent_id?: string | null`

    The unique identifier of the agent.

  - `base_template_id?: string | null`

    The base template ID that the step belongs to (cloud only).

  - `llm_request_ns?: number | null`

    Time spent on LLM requests in nanoseconds.

  - `llm_request_start_ns?: number | null`

    The timestamp of the start of the llm request in nanoseconds.

  - `project_id?: string | null`

    The project that the step belongs to (cloud only).

  - `provider_id?: string | null`

    The unique identifier of the provider.

  - `run_id?: string | null`

    The unique identifier of the run.

  - `step_ns?: number | null`

    Total time for the step in nanoseconds.

  - `step_start_ns?: number | null`

    The timestamp of the start of the step in nanoseconds.

  - `template_id?: string | null`

    The template ID that the step belongs to (cloud only).

  - `tool_execution_ns?: number | null`

    Time spent on tool execution in nanoseconds.
