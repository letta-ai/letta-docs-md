## Import Agent

`client.agents.importFile(AgentImportFileParamsparams, RequestOptionsoptions?): AgentImportFileResponse`

**post** `/v1/agents/import`

Import a serialized agent file and recreate the agent(s) in the system.
Returns the IDs of all imported agents.

### Parameters

- `params: AgentImportFileParams`

  - `file: Uploadable`

    Body param

  - `append_copy_suffix?: boolean`

    Body param: If set to True, appends "_copy" to the end of the agent name.

  - `embedding?: string | null`

    Body param: Embedding handle to override with.

  - `env_vars_json?: string | null`

    Body param: Environment variables as a JSON string to pass to the agent for tool execution. Use 'secrets' instead.

  - `model?: string | null`

    Body param: Model handle to override the agent's default model. This allows the imported agent to use a different model while keeping other defaults (e.g., context size) from the original configuration.

  - `name?: string | null`

    Body param: If provided, overrides the agent name with this value.

  - `override_embedding_handle?: string | null`

    Body param: Override import with specific embedding handle. Use 'embedding' instead.

  - `override_existing_tools?: boolean`

    Body param: If set to True, existing tools can get their source code overwritten by the uploaded tool definitions. Note that Letta core tools can never be updated externally.

  - `override_model_handle?: string | null`

    Body param: Model handle to override the agent's default model. Use 'model' instead.

  - `override_name?: string | null`

    Body param: If provided, overrides the agent name with this value. Use 'name' instead.

  - `project_id?: string | null`

    Body param: The project ID to associate the uploaded agent with. This is now passed via headers.

  - `secrets?: string | null`

    Body param: Secrets as a JSON string to pass to the agent for tool execution.

  - `strip_messages?: boolean`

    Body param: If set to True, strips all messages from the agent before importing.

  - `xOverrideEmbeddingModel?: string`

    Header param

### Returns

- `AgentImportFileResponse`

  Response model for imported agents

  - `agent_ids: Array<string>`

    List of IDs of the imported agents

### Example

```typescript
import fs from 'fs';
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.importFile({ file: fs.createReadStream('path/to/file') });

console.log(response.agent_ids);
```

#### Response

```json
{
  "agent_ids": [
    "string"
  ]
}
```
