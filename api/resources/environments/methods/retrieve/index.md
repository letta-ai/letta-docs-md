## Get Environment Connection

**get** `/v1/environments/{deviceId}`

Get a specific environment connection by deviceId

### Path Parameters

- `deviceId: string`

### Returns

- `id: string`

- `connectedAt: number`

- `connectionId: string`

- `connectionName: string`

- `deviceId: string`

- `firstSeenAt: number`

- `lastHeartbeat: number`

- `lastSeenAt: number`

- `organizationId: string`

- `podId: string`

- `apiKeyOwner: optional string`

- `currentMode: optional "default" or "standard" or "acceptEdits" or 2 more`

  - `"default"`

  - `"standard"`

  - `"acceptEdits"`

  - `"bypassPermissions"`

  - `"unrestricted"`

- `metadata: optional object { gitBranch, lettaCodeVersion, nodeVersion, 4 more }`

  - `gitBranch: optional string`

  - `lettaCodeVersion: optional string`

  - `nodeVersion: optional string`

  - `os: optional string`

  - `self_update: optional object { supported, writable, install_path, 2 more }`

    - `supported: boolean`

    - `writable: boolean`

    - `install_path: optional string`

    - `manual_command: optional string`

    - `reason: optional string`

  - `supported_commands: optional array of string`

  - `workingDirectory: optional string`

- `userId: optional string`

### Example

```http
curl https://api.letta.com/v1/environments/$DEVICE_ID \
    -H "Authorization: Bearer $LETTA_API_KEY"
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
