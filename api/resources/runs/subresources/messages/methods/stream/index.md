## Retrieve Stream For Run

**post** `/v1/runs/{run_id}/stream`

Retrieve Stream For Run

### Path Parameters

- `run_id: string`

### Body Parameters

- `agent_id: optional string`

  Agent ID for agent-direct mode with 'default' conversation. Use with conversation_id='default' in the URL path.

- `batch_size: optional number`

  Number of entries to read per batch.

- `include_pings: optional boolean`

  Whether to include periodic keepalive ping messages in the stream to prevent connection timeouts.

- `otid: optional string`

  Offline threading ID to look up the run_id. Bypasses active run lookup if run_id not provided.

- `poll_interval: optional number`

  Seconds to wait between polls when no new data.

- `run_id: optional string`

  Run ID to stream directly, bypassing run lookup. Use for recovery from duplicate requests.

- `starting_after: optional number`

  Sequence id to use as a cursor for pagination. Response will start streaming after this chunk sequence id

### Example

```http
curl https://api.letta.com/v1/runs/$RUN_ID/stream \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```
