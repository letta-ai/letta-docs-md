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
