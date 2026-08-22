## Export Agent

`client.agents.exportFile(stringagentID, AgentExportFileParamsquery?, RequestOptionsoptions?): AgentExportFileResponse`

**get** `/v1/agents/{agent_id}/export`

Export the serialized JSON representation of an agent, formatted with indentation.

### Parameters

- `agentID: string`

- `query: AgentExportFileParams`

  - `conversation_id?: string | null`

    Conversation ID to export. If provided, uses messages from this conversation instead of the agent's global message history.

  - `max_steps?: number`

  - `scrub_messages?: boolean`

    If True, excludes all messages from the export. Useful for sharing agent configs without conversation history.

  - `use_legacy_format?: boolean`

    If True, exports using the legacy single-agent 'v1' format with inline tools/blocks. If False, exports using the new multi-entity 'v2' format, with separate agents, tools, blocks, files, etc.

### Returns

- `AgentExportFileResponse = string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.exportFile('agent_id');

console.log(response);
```

#### Response

```json
"string"
```
