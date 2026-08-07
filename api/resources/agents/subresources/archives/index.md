# Archives

## Attach Archive To Agent

**patch** `/v1/agents/{agent_id}/archives/attach/{archive_id}`

Attach an archive to an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `archive_id: string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archives/attach/$ARCHIVE_ID \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## Detach Archive From Agent

**patch** `/v1/agents/{agent_id}/archives/detach/{archive_id}`

Detach an archive from an agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `archive_id: string`

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/archives/detach/$ARCHIVE_ID \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## Domain Types

### Archive Attach Response

- `ArchiveAttachResponse = unknown`

### Archive Detach Response

- `ArchiveDetachResponse = unknown`
