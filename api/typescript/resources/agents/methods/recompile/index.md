## Recompile Agent

`client.agents.recompile(stringagentID, AgentRecompileParamsparams?, RequestOptionsoptions?): AgentRecompileResponse`

**post** `/v1/agents/{agent_id}/recompile`

Manually trigger system prompt recompilation for an agent.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `params: AgentRecompileParams`

  - `dry_run?: boolean`

    If True, do not persist changes; still returns the compiled system prompt.

  - `update_timestamp?: boolean`

    If True, update the in-context memory last edit timestamp embedded in the system prompt.

### Returns

- `AgentRecompileResponse = string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.recompile('agent-123e4567-e89b-42d3-8456-426614174000');

console.log(response);
```

#### Response

```json
"string"
```
