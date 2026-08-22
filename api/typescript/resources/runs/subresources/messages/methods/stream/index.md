## Retrieve Stream For Run

`client.runs.messages.stream(stringrunID, MessageStreamParamsbody?, RequestOptionsoptions?): MessageStreamResponse | Stream<LettaStreamingResponse>`

**post** `/v1/runs/{run_id}/stream`

Retrieve Stream For Run

### Parameters

- `runID: string`

- `body: MessageStreamParams`

  - `agent_id?: string | null`

    Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

  - `batch_size?: number | null`

    Number of entries to read per batch.

  - `include_pings?: boolean | null`

    Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

  - `otid?: string | null`

    Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

  - `poll_interval?: number | null`

    Seconds to wait between polls when no new data.

  - `run_id?: string | null`

    Run ID to stream directly, bypassing run lookup. Use for recovery from duplicate requests.

  - `starting_after?: number`

    Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Returns

- `MessageStreamResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.runs.messages.stream('run_id');

console.log(response);
```

#### Response

```json
{}
```
