## Retrieve Usage For Run

**get** `/v1/runs/{run_id}/usage`

Get usage statistics for a run.

### Path Parameters

- `run_id: string`

### Returns

- `completion_tokens: optional number`

- `completion_tokens_details: optional object { reasoning_tokens }`

  - `reasoning_tokens: optional number`

- `prompt_tokens: optional number`

- `prompt_tokens_details: optional object { cache_creation_tokens, cache_read_tokens, cached_tokens }`

  - `cache_creation_tokens: optional number`

  - `cache_read_tokens: optional number`

  - `cached_tokens: optional number`

- `total_tokens: optional number`

### Example

```http
curl https://api.letta.com/v1/runs/$RUN_ID/usage \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "completion_tokens": 0,
  "completion_tokens_details": {
    "reasoning_tokens": 0
  },
  "prompt_tokens": 0,
  "prompt_tokens_details": {
    "cache_creation_tokens": 0,
    "cache_read_tokens": 0,
    "cached_tokens": 0
  },
  "total_tokens": 0
}
```
