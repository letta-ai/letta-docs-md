## Retrieve Trace For Run

**get** `/v1/runs/{run_id}/trace`

Retrieve OTEL trace spans for a run.

Returns a filtered set of spans relevant for observability:

- agent_step: Individual agent reasoning steps
- tool executions: Tool call spans
- Root span: The top-level request span
- time_to_first_token: TTFT measurement span

Requires ClickHouse to be configured for trace storage.

### Path Parameters

- `run_id: string`

### Query Parameters

- `limit: optional number`

  Maximum number of spans to return

### Example

```http
curl https://api.letta.com/v1/runs/$RUN_ID/trace \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  {
    "foo": "bar"
  }
]
```
