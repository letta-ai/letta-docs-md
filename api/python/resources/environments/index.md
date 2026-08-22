# Environments

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

## Send Message to Environment

`environments.send_message(strconnection_id, EnvironmentSendMessageParams**kwargs)  -> EnvironmentSendMessageResponse`

**post** `/v1/environments/{connectionId}/messages`

Send a message to a specific environment connection

### Parameters

- `connection_id: str`

- `messages: Iterable[Message]`

  - `class MessageUnionMember0: …`

    - `client_message_id: str`

    - `content: Union[str, Iterable[MessageUnionMember0ContentUnionMember1]]`

      - `str`

      - `Iterable[MessageUnionMember0ContentUnionMember1]`

        - `text: str`

        - `type: Literal["text"]`

          - `"text"`

    - `role: Literal["user"]`

      - `"user"`

    - `otid: Optional[str]`

  - `class MessageUnionMember1: …`

    - `approvals: Iterable[MessageUnionMember1Approval]`

      - `class MessageUnionMember1ApprovalUnionMember0: …`

        - `status: Literal["success", "error"]`

          - `"success"`

          - `"error"`

        - `tool_call_id: str`

        - `tool_return: Union[str, Iterable[MessageUnionMember1ApprovalUnionMember0ToolReturnUnionMember1]]`

          - `str`

          - `Iterable[MessageUnionMember1ApprovalUnionMember0ToolReturnUnionMember1]`

            - `text: str`

            - `type: Literal["text"]`

              - `"text"`

        - `stderr: Optional[Sequence[str]]`

        - `stdout: Optional[Sequence[str]]`

        - `type: Optional[Literal["tool"]]`

          - `"tool"`

      - `class MessageUnionMember1ApprovalUnionMember1: …`

        - `approve: bool`

        - `tool_call_id: str`

        - `reason: Optional[str]`

        - `type: Optional[Literal["approval"]]`

          - `"approval"`

        - `updated_input: Optional[Dict[str, object]]`

    - `type: Literal["approval"]`

      - `"approval"`

- `agent_id: Optional[str]`

- `conversation_id: Optional[str]`

### Returns

- `class EnvironmentSendMessageResponse: …`

  - `message: str`

  - `success: bool`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.environments.send_message(
    connection_id="connectionId",
    messages=[{
        "client_message_id": "client_message_id",
        "content": "string",
        "role": "user",
    }],
)
print(response.message)
```

#### Response

```json
{
  "message": "message",
  "success": true
}
```

## Domain Types

### Environment List Response

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

### Environment Retrieve Response

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

### Environment Send Message Response

- `class EnvironmentSendMessageResponse: …`

  - `message: str`

  - `success: bool`
