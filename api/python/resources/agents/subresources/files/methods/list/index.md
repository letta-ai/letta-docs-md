## List Files For Agent

`agents.files.list(stragent_id, FileListParams**kwargs)  -> SyncNextFilesPage[FileListResponse]`

**get** `/v1/agents/{agent_id}/files`

Get the files attached to an agent with their open/closed status.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `after: Optional[str]`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `cursor: Optional[str]`

  Pagination cursor from previous response (deprecated, use before/after)

- `is_open: Optional[bool]`

  Filter by open status (true for open files, false for closed files)

- `limit: Optional[int]`

  Maximum number of files to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for files by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `class FileListResponse: …`

  Response model for agent file attachments showing file status in agent context

  - `id: str`

    Unique identifier of the file-agent relationship

  - `file_id: str`

    Unique identifier of the file

  - `file_name: str`

    Name of the file

  - `folder_id: str`

    Unique identifier of the folder/source

  - `folder_name: str`

    Name of the folder/source

  - `is_open: bool`

    Whether the file is currently open in the agent's context

  - `end_line: Optional[int]`

    Ending line number if file was opened with line range

  - `last_accessed_at: Optional[datetime]`

    Timestamp of last access by the agent

  - `start_line: Optional[int]`

    Starting line number if file was opened with line range

  - `visible_content: Optional[str]`

    Portion of the file visible to the agent if open

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.agents.files.list(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
page = page.files[0]
print(page.id)
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
