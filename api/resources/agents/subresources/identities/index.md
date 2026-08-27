# Identities

## Attach Identity To Agent

**patch** `/v1/agents/{agent_id}/identities/attach/{identity_id}`

Attach an identity to an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `identity_id: string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/identities/attach/$IDENTITY_ID \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## Detach Identity From Agent

**patch** `/v1/agents/{agent_id}/identities/detach/{identity_id}`

Detach an identity from an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `identity_id: string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/identities/detach/$IDENTITY_ID \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
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
