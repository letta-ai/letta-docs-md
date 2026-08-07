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
