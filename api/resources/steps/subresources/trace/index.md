# Trace

## Retrieve Trace For Step

**get** `/v1/steps/{step_id}/trace`

Retrieve Trace For Step

### Path Parameters

- `step_id: string`

  The ID of the step in the format 'step-<uuid4>'

### Returns

- `ProviderTrace object { request_json, response_json, id, 15 more }`

  Letta's internal representation of a provider trace.

  Attributes:
  id (str): The unique identifier of the provider trace.
  request_json (Dict[str, Any]): JSON content of the provider request.
  response_json (Dict[str, Any]): JSON content of the provider response.
  step_id (str): ID of the step that this trace is associated with.
  agent_id (str): ID of the agent that generated this trace.
  agent_tags (list[str]): Tags associated with the agent for filtering.
  call_type (str): Type of call (agent_step, summarization, etc.).
  run_id (str): ID of the run this trace is associated with.
  source (str): Source service that generated this trace (memgpt-server, lettuce-py).
  organization_id (str): The unique identifier of the organization.
  user_id (str): The unique identifier of the user who initiated the request.
  compaction_settings (Dict[str, Any]): Compaction/summarization settings (only for summarization calls).
  llm_config (Dict[str, Any]): LLM configuration used for this call (only for non-summarization calls).
  created_at (datetime): The timestamp when the object was created.

  - `request_json: map[unknown]`

    JSON content of the provider request

  - `response_json: map[unknown]`

    JSON content of the provider response

  - `id: optional string`

    The human-friendly ID of the Provider_trace

  - `agent_id: optional string`

    ID of the agent that generated this trace

  - `agent_tags: optional array of string`

    Tags associated with the agent for filtering

  - `billing_context: optional object { cost_source, customer_id, plan_type }`

    Billing context for LLM request cost tracking.

    - `cost_source: optional string`

      Cost source: 'quota' or 'credits'

    - `customer_id: optional string`

      Customer ID for billing records

    - `plan_type: optional string`

      Subscription tier

  - `call_type: optional string`

    Type of call (agent_step, summarization, etc.)

  - `compaction_settings: optional map[unknown]`

    Compaction/summarization settings (summarization calls only)

  - `created_at: optional string`

    The timestamp when the object was created.

  - `created_by_id: optional string`

    The id of the user that made this object.

  - `last_updated_by_id: optional string`

    The id of the user that made this object.

  - `latency_ms: optional number`

    LLM request latency in milliseconds

  - `llm_config: optional map[unknown]`

    LLM configuration used for this call (non-summarization calls only)

  - `org_id: optional string`

    ID of the organization

  - `run_id: optional string`

    ID of the run this trace is associated with

  - `source: optional string`

    Source service that generated this trace (memgpt-server, lettuce-py)

  - `step_id: optional string`

    ID of the step that this trace is associated with

  - `updated_at: optional string`

    The timestamp when the object was last updated.

### Example

```http
curl https://api.letta.com/v1/steps/$STEP_ID/trace \
    -H "Authorization: Bearer $LETTA_API_KEY"
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
