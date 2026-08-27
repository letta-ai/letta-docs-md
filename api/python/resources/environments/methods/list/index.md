## List Environment Connections

`environments.list(EnvironmentListParams**kwargs)  -> EnvironmentListResponse`

**get** `/v1/environments`

List all active environment connections for the organization

### Parameters

- `after: Optional[str]`

- `limit: Optional[str]`

- `online_only: Optional[str]`

- `source: Optional[Literal["local", "remote"]]`

  - `"local"`

  - `"remote"`

- `user_id: Optional[str]`

### Returns

- `class EnvironmentListResponse: …`

  - `connections: List[Connection]`

    - `id: str`

    - `connected_at: Optional[float]`

    - `connection_id: Optional[str]`

    - `connection_name: str`

    - `device_id: str`

    - `first_seen_at: float`

    - `last_heartbeat: Optional[float]`

    - `last_seen_at: float`

    - `organization_id: str`

    - `pod_id: Optional[str]`

    - `api_key_owner: Optional[str]`

    - `current_mode: Optional[Literal["default", "standard", "acceptEdits", 2 more]]`

      - `"default"`

      - `"standard"`

      - `"acceptEdits"`

      - `"bypassPermissions"`

      - `"unrestricted"`

    - `metadata: Optional[ConnectionMetadata]`

      - `git_branch: Optional[str]`

      - `letta_code_version: Optional[str]`

      - `node_version: Optional[str]`

      - `os: Optional[str]`

      - `self_update: Optional[ConnectionMetadataSelfUpdate]`

        - `supported: bool`

        - `writable: bool`

        - `install_path: Optional[str]`

        - `manual_command: Optional[str]`

        - `reason: Optional[str]`

      - `supported_commands: Optional[List[str]]`

      - `working_directory: Optional[str]`

    - `user_id: Optional[str]`

  - `has_next_page: bool`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
environments = client.environments.list()
print(environments.connections)
```

#### Response

```json
{
  "connections": [
    {
      "id": "id",
      "connectedAt": 0,
      "connectionId": "connectionId",
      "connectionName": "connectionName",
      "deviceId": "deviceId",
      "firstSeenAt": 0,
      "lastHeartbeat": 0,
      "lastSeenAt": 0,
      "organizationId": "organizationId",
      "podId": "podId",
      "apiKeyOwner": "apiKeyOwner",
      "currentMode": "default",
      "metadata": {
        "gitBranch": "gitBranch",
        "lettaCodeVersion": "lettaCodeVersion",
        "nodeVersion": "nodeVersion",
        "os": "os",
        "self_update": {
          "supported": true,
          "writable": true,
          "install_path": "install_path",
          "manual_command": "manual_command",
          "reason": "reason"
        },
        "supported_commands": [
          "string"
        ],
        "workingDirectory": "workingDirectory"
      },
      "userId": "userId"
    }
  ],
  "hasNextPage": true
}
```
