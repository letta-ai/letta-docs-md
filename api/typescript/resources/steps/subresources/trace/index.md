# Trace

## Retrieve Trace For Step

`client.steps.trace.retrieve(stringstepID, RequestOptionsoptions?): ProviderTrace | null`

**get** `/v1/steps/{step_id}/trace`

Retrieve Trace For Step

### Parameters

- `stepID: string`

  The ID of the step in the format 'step-<uuid4>'

### Returns

- `ProviderTrace | null`

  - `request_json: Record<string, unknown>`

    JSON content of the provider request

  - `response_json: Record<string, unknown>`

    JSON content of the provider response

  - `id?: string`

    The human-friendly ID of the Provider_trace

  - `agent_id?: string | null`

    ID of the agent that generated this trace

  - `agent_tags?: Array<string> | null`

    Tags associated with the agent for filtering

  - `billing_context?: BillingContext | null`

    Billing context for LLM request cost tracking.

    - `cost_source?: string | null`

      Cost source: 'quota' or 'credits'

    - `customer_id?: string | null`

      Customer ID for billing records

    - `plan_type?: string | null`

      Subscription tier

  - `call_type?: string | null`

    Type of call (agent_step, summarization, etc.)

  - `compaction_settings?: Record<string, unknown> | null`

    Compaction/summarization settings (summarization calls only)

  - `created_at?: string`

    The timestamp when the object was created.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `latency_ms?: number | null`

    LLM request latency in milliseconds

  - `llm_config?: Record<string, unknown> | null`

    LLM configuration used for this call (non-summarization calls only)

  - `org_id?: string | null`

    ID of the organization

  - `run_id?: string | null`

    ID of the run this trace is associated with

  - `source?: string | null`

    Source service that generated this trace (memgpt-server, lettuce-py)

  - `step_id?: string | null`

    ID of the step that this trace is associated with

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const providerTrace = await client.steps.trace.retrieve(
  'step-123e4567-e89b-42d3-8456-426614174000',
);

console.log(providerTrace.id);
```

#### Response

```json
{
  "request_json": {
    "foo": "bar"
  },
  "response_json": {
    "foo": "bar"
  },
  "id": "provider_trace-123e4567-e89b-12d3-a456-426614174000",
  "agent_id": "agent_id",
  "agent_tags": [
    "string"
  ],
  "billing_context": {
    "cost_source": "cost_source",
    "customer_id": "customer_id",
    "plan_type": "plan_type"
  },
  "call_type": "call_type",
  "compaction_settings": {
    "foo": "bar"
  },
  "created_at": "2019-12-27T18:11:19.117Z",
  "created_by_id": "created_by_id",
  "last_updated_by_id": "last_updated_by_id",
  "latency_ms": 0,
  "llm_config": {
    "foo": "bar"
  },
  "org_id": "org_id",
  "run_id": "run_id",
  "source": "source",
  "step_id": "step_id",
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```
