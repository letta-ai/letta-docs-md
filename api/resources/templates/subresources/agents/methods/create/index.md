## Create Agents From Template

**post** `/v1/templates/{template_version}/agents`

Creates an Agent or multiple Agents from a template

### Path Parameters

- `template_version: string`

### Body Parameters

- `agent_name: optional string`

  The name of the agent, optional otherwise a random one will be assigned

- `identity_ids: optional array of string`

  The identity ids to assign to the agent

- `initial_message_sequence: optional array of object { content, role, batch_item_id, 4 more }`

  Set an initial sequence of messages, if not provided, the agent will start with the default message sequence, if an empty array is provided, the agent will start with no messages

  - `content: string`

  - `role: "user" or "system" or "assistant"`

    - `"user"`

    - `"system"`

    - `"assistant"`

  - `batch_item_id: optional string`

  - `group_id: optional string`

  - `name: optional string`

  - `otid: optional string`

  - `sender_id: optional string`

- `memory_variables: optional map[string]`

  The memory variables to assign to the agent

- `tags: optional array of string`

  The tags to assign to the agent

- `tool_variables: optional map[string]`

  The tool variables to assign to the agent

### Returns

- `agent_ids: array of string`

  Array of created agent IDs

- `deployment_id: string`

  The deployment ID for the created agents

- `group_id: string`

  Optional group ID if agents were created in a group

### Example

```http
curl https://api.letta.com/v1/templates/$TEMPLATE_VERSION/agents \
    -X POST \
    -H "Authorization: Bearer $LETTA_API_KEY"
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
