# Agents

## Create Agents From Template

`client.templates.agents.create(stringtemplateVersion, AgentCreateParamsbody?, RequestOptionsoptions?): AgentCreateResponse`

**post** `/v1/templates/{template_version}/agents`

Creates an Agent or multiple Agents from a template

### Parameters

- `templateVersion: string`

- `body: AgentCreateParams`

  - `agent_name?: string`

    The name of the agent, optional otherwise a random one will be assigned

  - `identity_ids?: Array<string>`

    The identity ids to assign to the agent

  - `initial_message_sequence?: Array<InitialMessageSequence>`

    Set an initial sequence of messages, if not provided, the agent will start with the default message sequence, if an empty array is provided, the agent will start with no messages

    - `content: string`

    - `role: "user" | "system" | "assistant"`

      - `"user"`

      - `"system"`

      - `"assistant"`

    - `batch_item_id?: string | null`

    - `group_id?: string | null`

    - `name?: string | null`

    - `otid?: string | null`

    - `sender_id?: string | null`

  - `memory_variables?: Record<string, string>`

    The memory variables to assign to the agent

  - `tags?: Array<string>`

    The tags to assign to the agent

  - `tool_variables?: Record<string, string>`

    The tool variables to assign to the agent

### Returns

- `AgentCreateResponse`

  Response containing created agent IDs and associated metadata

  - `agent_ids: Array<string>`

    Array of created agent IDs

  - `deployment_id: string`

    The deployment ID for the created agents

  - `group_id: string | null`

    Optional group ID if agents were created in a group

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const agent = await client.templates.agents.create('template_version');

console.log(agent.agent_ids);
```

#### Response

```json
{
  "agent_ids": [
    "string"
  ],
  "deployment_id": "deployment_id",
  "group_id": "group_id"
}
```

## Domain Types

### Agent Create Response

- `AgentCreateResponse`

  Response containing created agent IDs and associated metadata

  - `agent_ids: Array<string>`

    Array of created agent IDs

  - `deployment_id: string`

    The deployment ID for the created agents

  - `group_id: string | null`

    Optional group ID if agents were created in a group
