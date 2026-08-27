## Retrieve Usage For Run

`runs.usage.retrieve(strrun_id)  -> UsageRetrieveResponse`

**get** `/v1/runs/{run_id}/usage`

Get usage statistics for a run.

### Parameters

- `run_id: str`

### Returns

- `class UsageRetrieveResponse: …`

  - `completion_tokens: Optional[int]`

  - `completion_tokens_details: Optional[CompletionTokensDetails]`

    - `reasoning_tokens: Optional[int]`

  - `prompt_tokens: Optional[int]`

  - `prompt_tokens_details: Optional[PromptTokensDetails]`

    - `cache_creation_tokens: Optional[int]`

    - `cache_read_tokens: Optional[int]`

    - `cached_tokens: Optional[int]`

  - `total_tokens: Optional[int]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
usage = client.runs.usage.retrieve(
    "run_id",
)
print(usage.completion_tokens)
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
