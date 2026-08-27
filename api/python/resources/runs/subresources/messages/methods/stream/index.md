## Retrieve Stream For Run

`runs.messages.stream(strpath_run_id, MessageStreamParams**kwargs)  -> object`

**post** `/v1/runs/{run_id}/stream`

Retrieve Stream For Run

### Parameters

- `run_id: str`

- `agent_id: Optional[str]`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `batch_size: Optional[int]`

  Number of entries to read per batch.

- `include_pings: Optional[bool]`

  Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

- `otid: Optional[str]`

  Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

- `poll_interval: Optional[float]`

  Seconds to wait between polls when no new data.

- `run_id: str`

- `starting_after: Optional[int]`

  Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
for message in client.runs.messages.stream(
    path_run_id="run_id",
):
  print(message)
```

#### Response

```json
{}
```
