# Environments

## List Environment Connections

**get** `/v1/environments`

List all active environment connections for the organization

### Query Parameters

- `after: optional string`

- `limit: optional string`

- `onlineOnly: optional string`

- `source: optional "local" or "remote"`

  - `"local"`

  - `"remote"`

- `userId: optional string`

### Returns

- `connections: array of object { id, connectedAt, connectionId, 11 more }`

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

- `hasNextPage: boolean`

### Example

```http
curl https://api.letta.com/v1/environments \
    -H "Authorization: Bearer $LETTA_API_KEY"
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

## Send Message to Environment

**post** `/v1/environments/{connectionId}/messages`

Send a message to a specific environment connection

### Path Parameters

- `connectionId: string`

### Body Parameters

- `messages: array of object { client_message_id, content, role, otid }  or object { approvals, type }`

  - `object { client_message_id, content, role, otid }`

    - `client_message_id: string`

    - `content: string or array of object { text, type }`

      - `string`

      - `array of object { text, type }`

        - `text: string`

        - `type: "text"`

          - `"text"`

    - `role: "user"`

      - `"user"`

    - `otid: optional string`

  - `object { approvals, type }`

    - `approvals: array of object { status, tool_call_id, tool_return, 3 more }  or object { approve, tool_call_id, reason, 2 more }`

      - `object { status, tool_call_id, tool_return, 3 more }`

        - `status: "success" or "error"`

          - `"success"`

          - `"error"`

        - `tool_call_id: string`

        - `tool_return: string or array of object { text, type }`

          - `string`

          - `array of object { text, type }`

            - `text: string`

            - `type: "text"`

              - `"text"`

        - `stderr: optional array of string`

        - `stdout: optional array of string`

        - `type: optional "tool"`

          - `"tool"`

      - `object { approve, tool_call_id, reason, 2 more }`

        - `approve: boolean`

        - `tool_call_id: string`

        - `reason: optional string`

        - `type: optional "approval"`

          - `"approval"`

        - `updated_input: optional map[unknown]`

    - `type: "approval"`

      - `"approval"`

- `agentId: optional string`

- `conversationId: optional string`

### Returns

- `message: string`

- `success: boolean`

### Example

```http
curl https://api.letta.com/v1/environments/$CONNECTION_ID/messages \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $LETTA_API_KEY" \
    -d '{
          "messages": [
            {
              "client_message_id": "client_message_id",
              "content": "string",
              "role": "user"
            }
          ]
        }'
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

- `EnvironmentListResponse object { connections, hasNextPage }`

  - `connections: array of object { id, connectedAt, connectionId, 11 more }`

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

  - `hasNextPage: boolean`

### Environment Retrieve Response

- `EnvironmentRetrieveResponse object { id, connectedAt, connectionId, 11 more }`

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

### Environment Send Message Response

- `EnvironmentSendMessageResponse object { message, success }`

  - `message: string`

  - `success: boolean`
