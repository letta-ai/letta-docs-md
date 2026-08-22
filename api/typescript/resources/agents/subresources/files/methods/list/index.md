## List Files For Agent

`client.agents.files.list(stringagentID, FileListParamsquery?, RequestOptionsoptions?): NextFilesPage<FileListResponse>`

**get** `/v1/agents/{agent_id}/files`

Get the files attached to an agent with their open/closed status.

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `query: FileListParams`

  - `after?: string | null`

    Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

  - `cursor?: string | null`

    Pagination cursor from previous response (deprecated, use before/after)

  - `is_open?: boolean | null`

    Filter by open status (true for open files, false for closed files)

  - `limit?: number | null`

    Maximum number of files to return

  - `order?: "asc" | "desc"`

    Sort order for files by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `FileListResponse`

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

  - `end_line?: number | null`

    Ending line number if file was opened with line range

  - `last_accessed_at?: string | null`

    Timestamp of last access by the agent

  - `start_line?: number | null`

    Starting line number if file was opened with line range

  - `visible_content?: string | null`

    Portion of the file visible to the agent if open

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const fileListResponse of client.agents.files.list(
  'agent-123e4567-e89b-42d3-8456-426614174000',
)) {
  console.log(fileListResponse.id);
}
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
