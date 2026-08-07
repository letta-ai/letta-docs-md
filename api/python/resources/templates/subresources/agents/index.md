# Agents

## Create Agents From Template

`templates.agents.create(strtemplate_version, AgentCreateParams**kwargs)  -> AgentCreateResponse`

**post** `/v1/templates/{template_version}/agents`

Creates an Agent or multiple Agents from a template

### Parameters

- `template_version: str`

- `agent_name: Optional[str]`

  The name of the agent, optional otherwise a random one will be assigned

- `identity_ids: Optional[Sequence[str]]`

  The identity ids to assign to the agent

- `initial_message_sequence: Optional[Iterable[InitialMessageSequence]]`

  Set an initial sequence of messages, if not provided, the agent will start with the default message sequence, if an empty array is provided, the agent will start with no messages

  - `content: str`

  - `role: Literal["user", "system", "assistant"]`

    - `"user"`

    - `"system"`

    - `"assistant"`

  - `batch_item_id: Optional[str]`

  - `group_id: Optional[str]`

  - `name: Optional[str]`

  - `otid: Optional[str]`

  - `sender_id: Optional[str]`

- `memory_variables: Optional[Dict[str, str]]`

  The memory variables to assign to the agent

- `tags: Optional[Sequence[str]]`

  The tags to assign to the agent

- `tool_variables: Optional[Dict[str, str]]`

  The tool variables to assign to the agent

### Returns

- `class AgentCreateResponse: …`

  Response containing created agent IDs and associated metadata

  - `agent_ids: List[str]`

    Array of created agent IDs

  - `deployment_id: str`

    The deployment ID for the created agents

  - `group_id: Optional[str]`

    Optional group ID if agents were created in a group

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
agent = client.templates.agents.create(
    template_version="template_version",
)
print(agent.agent_ids)
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

- `class AgentCreateResponse: …`

  Response containing created agent IDs and associated metadata

  - `agent_ids: List[str]`

    Array of created agent IDs

  - `deployment_id: str`

    The deployment ID for the created agents

  - `group_id: Optional[str]`

    Optional group ID if agents were created in a group
