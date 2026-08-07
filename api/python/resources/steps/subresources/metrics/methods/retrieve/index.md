## Retrieve Metrics For Step

`steps.metrics.retrieve(strstep_id)  -> MetricRetrieveResponse`

**get** `/v1/steps/{step_id}/metrics`

Get step metrics by step ID.

### Parameters

- `step_id: str`

  The ID of the step in the format 'step-<uuid4>'

### Returns

- `class MetricRetrieveResponse: …`

  - `id: str`

    The id of the step this metric belongs to (matches steps.id).

  - `agent_id: Optional[str]`

    The unique identifier of the agent.

  - `base_template_id: Optional[str]`

    The base template ID that the step belongs to (cloud only).

  - `llm_request_ns: Optional[int]`

    Time spent on LLM requests in nanoseconds.

  - `llm_request_start_ns: Optional[int]`

    The timestamp of the start of the llm request in nanoseconds.

  - `project_id: Optional[str]`

    The project that the step belongs to (cloud only).

  - `provider_id: Optional[str]`

    The unique identifier of the provider.

  - `run_id: Optional[str]`

    The unique identifier of the run.

  - `step_ns: Optional[int]`

    Total time for the step in nanoseconds.

  - `step_start_ns: Optional[int]`

    The timestamp of the start of the step in nanoseconds.

  - `template_id: Optional[str]`

    The template ID that the step belongs to (cloud only).

  - `tool_execution_ns: Optional[int]`

    Time spent on tool execution in nanoseconds.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
metric = client.steps.metrics.retrieve(
    "step-123e4567-e89b-42d3-8456-426614174000",
)
print(metric.id)
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
