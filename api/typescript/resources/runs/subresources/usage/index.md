# Usage

## Retrieve Usage For Run

`client.runs.usage.retrieve(stringrunID, RequestOptionsoptions?): UsageRetrieveResponse`

**get** `/v1/runs/{run_id}/usage`

Get usage statistics for a run.

### Parameters

- `runID: string`

### Returns

- `UsageRetrieveResponse`

  - `completion_tokens?: number`

  - `completion_tokens_details?: CompletionTokensDetails | null`

    - `reasoning_tokens?: number | null`

  - `prompt_tokens?: number`

  - `prompt_tokens_details?: PromptTokensDetails | null`

    - `cache_creation_tokens?: number | null`

    - `cache_read_tokens?: number | null`

    - `cached_tokens?: number | null`

  - `total_tokens?: number`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const usage = await client.runs.usage.retrieve('run_id');

console.log(usage.completion_tokens);
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

## Domain Types

### Usage Retrieve Response

- `UsageRetrieveResponse`

  - `completion_tokens?: number`

  - `completion_tokens_details?: CompletionTokensDetails | null`

    - `reasoning_tokens?: number | null`

  - `prompt_tokens?: number`

  - `prompt_tokens_details?: PromptTokensDetails | null`

    - `cache_creation_tokens?: number | null`

    - `cache_read_tokens?: number | null`

    - `cached_tokens?: number | null`

  - `total_tokens?: number`
