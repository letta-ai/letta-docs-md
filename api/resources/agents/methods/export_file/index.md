## Export Agent

**get** `/v1/agents/{agent_id}/export`

Export the serialized JSON representation of an agent, formatted with indentation.

### Path Parameters

- `agent_id: string`

### Query Parameters

- `conversation_id: optional string`

  Conversation ID to export. If provided, uses messages from this conversation instead of the agent's global message history.

- `max_steps: optional number`

- `scrub_messages: optional boolean`

  If True, excludes all messages from the export. Useful for sharing agent configs without conversation history.

- `use_legacy_format: optional boolean`

  If True, exports using the legacy single-agent 'v1' format with inline tools/blocks. If False, exports using the new multi-entity 'v2' format, with separate agents, tools, blocks, files, etc.

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/export \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
"string"
```
