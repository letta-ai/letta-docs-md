# Identities

## Attach Identity To Agent

`client.agents.identities.attach(stringidentityID, IdentityAttachParamsparams, RequestOptionsoptions?): IdentityAttachResponse`

**patch** `/v1/agents/{agent_id}/identities/attach/{identity_id}`

Attach an identity to an agent.

### Parameters

- `identityID: string`

- `params: IdentityAttachParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `IdentityAttachResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.identities.attach('identity_id', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(response);
```

#### Response

```json
{}
```

## Detach Identity From Agent

`client.agents.identities.detach(stringidentityID, IdentityDetachParamsparams, RequestOptionsoptions?): IdentityDetachResponse`

**patch** `/v1/agents/{agent_id}/identities/detach/{identity_id}`

Detach an identity from an agent.

### Parameters

- `identityID: string`

- `params: IdentityDetachParams`

  - `agent_id: string`

    The ID of the agent in the format 'agent-<uuid4>'

### Returns

- `IdentityDetachResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.agents.identities.detach('identity_id', {
  agent_id: 'agent-123e4567-e89b-42d3-8456-426614174000',
});

console.log(response);
```

#### Response

```json
{}
```

## Domain Types

### Identity Attach Response

- `IdentityAttachResponse = unknown`

### Identity Detach Response

- `IdentityDetachResponse = unknown`
