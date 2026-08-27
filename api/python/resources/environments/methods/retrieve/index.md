## Get Environment Connection

`environments.retrieve(strdevice_id)  -> EnvironmentRetrieveResponse`

**get** `/v1/environments/{deviceId}`

Get a specific environment connection by deviceId

### Parameters

- `device_id: str`

### Returns

- `class EnvironmentRetrieveResponse: …`

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

  - `metadata: Optional[Metadata]`

    - `git_branch: Optional[str]`

    - `letta_code_version: Optional[str]`

    - `node_version: Optional[str]`

    - `os: Optional[str]`

    - `self_update: Optional[MetadataSelfUpdate]`

      - `supported: bool`

      - `writable: bool`

      - `install_path: Optional[str]`

      - `manual_command: Optional[str]`

      - `reason: Optional[str]`

    - `supported_commands: Optional[List[str]]`

    - `working_directory: Optional[str]`

  - `user_id: Optional[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
environment = client.environments.retrieve(
    "deviceId",
)
print(environment.id)
```

#### Response

```json
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
```
