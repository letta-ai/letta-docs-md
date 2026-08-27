# Files

## Close All Files For Agent

**patch** `/v1/agents/{agent_id}/files/close-all`

Closes all currently open files for a given agent.

This endpoint updates the file state for the agent so that no files are marked as open.
Typically used to reset the working memory view for the agent.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/files/close-all \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  "string"
]
```

## Open File For Agent

**patch** `/v1/agents/{agent_id}/files/{file_id}/open`

Opens a specific file for a given agent.

This endpoint marks a specific file as open in the agent's file state.
The file will be included in the agent's working memory view.
Returns a list of file names that were closed due to LRU eviction.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `file_id: string`

  The ID of the file in the format 'file-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/files/$FILE_ID/open \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
[
  "string"
]
```

## Close File For Agent

**patch** `/v1/agents/{agent_id}/files/{file_id}/close`

Closes a specific file for a given agent.

This endpoint marks a specific file as closed in the agent's file state.
The file will be removed from the agent's working memory view.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `file_id: string`

  The ID of the file in the format 'file-<uuid4>'

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/files/$FILE_ID/close \
    -X PATCH \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{}
```

## List Files For Agent

**get** `/v1/agents/{agent_id}/files`

Get the files attached to an agent with their open/closed status.

### Path Parameters

- `agent_id: string`

  The ID of the agent in the format 'agent-<uuid4>'

### Query Parameters

- `after: optional string`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `before: optional string`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `cursor: optional string`

  Pagination cursor from previous response (deprecated, use before/after)

- `is_open: optional boolean`

  Filter by open status (true for open files, false for closed files)

- `limit: optional number`

  Maximum number of files to return

- `order: optional "asc" or "desc"`

  Sort order for files by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: optional "created_at"`

  Field to sort by

  - `"created_at"`

### Returns

- `files: array of object { id, file_id, file_name, 7 more }`

  List of file attachments for the agent

  - `id: string`

    Unique identifier of the file-agent relationship

  - `file_id: string`

    Unique identifier of the file

  - `file_name: string`

    Name of the file

  - `folder_id: string`

    Unique identifier of the folder/source

  - `folder_name: string`

    Name of the folder/source

  - `is_open: boolean`

    Whether the file is currently open in the agent's context

  - `end_line: optional number`

    Ending line number if file was opened with line range

  - `last_accessed_at: optional string`

    Timestamp of last access by the agent

  - `start_line: optional number`

    Starting line number if file was opened with line range

  - `visible_content: optional string`

    Portion of the file visible to the agent if open

- `has_more: boolean`

  Whether more results exist after this page

- `next_cursor: optional string`

  Cursor for fetching the next page (file-agent relationship ID)

### Example

```http
curl https://api.letta.com/v1/agents/$AGENT_ID/files \
    -H "Authorization: Bearer $LETTA_API_KEY"
```

#### Response

```json
{
  "files": [
    {
      "id": "id",
      "file_id": "file_id",
      "file_name": "file_name",
      "folder_id": "folder_id",
      "folder_name": "folder_name",
      "is_open": true,
      "end_line": 0,
      "last_accessed_at": "2019-12-27T18:11:19.117Z",
      "start_line": 0,
      "visible_content": "visible_content"
    }
  ],
  "has_more": true,
  "next_cursor": "next_cursor"
}
```

## Domain Types

### File Close All Response

- `FileCloseAllResponse = array of string`

### File Open Response

- `FileOpenResponse = array of string`

### File Close Response

- `FileCloseResponse = unknown`

### File List Response

- `FileListResponse object { id, file_id, file_name, 7 more }`

  Response model for agent file attachments showing file status in agent context

  - `id: string`

    Unique identifier of the file-agent relationship

  - `file_id: string`

    Unique identifier of the file

  - `file_name: string`

    Name of the file

  - `folder_id: string`

    Unique identifier of the folder/source

  - `folder_name: string`

    Name of the folder/source

  - `is_open: boolean`

    Whether the file is currently open in the agent's context

  - `end_line: optional number`

    Ending line number if file was opened with line range

  - `last_accessed_at: optional string`

    Timestamp of last access by the agent

  - `start_line: optional number`

    Starting line number if file was opened with line range

  - `visible_content: optional string`

    Portion of the file visible to the agent if open
