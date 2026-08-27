# Environments

## List Environment Connections

`client.environments.list(EnvironmentListParamsquery?, RequestOptionsoptions?): EnvironmentListResponse`

**get** `/v1/environments`

List all active environment connections for the organization

### Parameters

- `query: EnvironmentListParams`

  - `after?: string`

  - `limit?: string`

  - `onlineOnly?: string`

  - `source?: "local" | "remote"`

    - `"local"`

    - `"remote"`

  - `userId?: string`

### Returns

- `EnvironmentListResponse`

  - `connections: Array<Connection>`

    - `id: string`

    - `connectedAt: number | null`

    - `connectionId: string | null`

    - `connectionName: string`

    - `deviceId: string`

    - `firstSeenAt: number`

    - `lastHeartbeat: number | null`

    - `lastSeenAt: number`

    - `organizationId: string`

    - `podId: string | null`

    - `apiKeyOwner?: string`

    - `currentMode?: "default" | "standard" | "acceptEdits" | 2 more`

      - `"default"`

      - `"standard"`

      - `"acceptEdits"`

      - `"bypassPermissions"`

      - `"unrestricted"`

    - `metadata?: Metadata`

      - `gitBranch?: string`

      - `lettaCodeVersion?: string`

      - `nodeVersion?: string`

      - `os?: string`

      - `self_update?: SelfUpdate`

        - `supported: boolean`

        - `writable: boolean`

        - `install_path?: string`

        - `manual_command?: string`

        - `reason?: string`

      - `supported_commands?: Array<string>`

      - `workingDirectory?: string`

    - `userId?: string`

  - `hasNextPage: boolean`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const environments = await client.environments.list();

console.log(environments.connections);
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

`client.environments.retrieve(stringdeviceID, RequestOptionsoptions?): EnvironmentRetrieveResponse`

**get** `/v1/environments/{deviceId}`

Get a specific environment connection by deviceId

### Parameters

- `deviceID: string`

### Returns

- `EnvironmentRetrieveResponse`

  - `id: string`

  - `connectedAt: number | null`

  - `connectionId: string | null`

  - `connectionName: string`

  - `deviceId: string`

  - `firstSeenAt: number`

  - `lastHeartbeat: number | null`

  - `lastSeenAt: number`

  - `organizationId: string`

  - `podId: string | null`

  - `apiKeyOwner?: string`

  - `currentMode?: "default" | "standard" | "acceptEdits" | 2 more`

    - `"default"`

    - `"standard"`

    - `"acceptEdits"`

    - `"bypassPermissions"`

    - `"unrestricted"`

  - `metadata?: Metadata`

    - `gitBranch?: string`

    - `lettaCodeVersion?: string`

    - `nodeVersion?: string`

    - `os?: string`

    - `self_update?: SelfUpdate`

      - `supported: boolean`

      - `writable: boolean`

      - `install_path?: string`

      - `manual_command?: string`

      - `reason?: string`

    - `supported_commands?: Array<string>`

    - `workingDirectory?: string`

  - `userId?: string`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const environment = await client.environments.retrieve('deviceId');

console.log(environment.id);
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

`client.environments.sendMessage(stringconnectionID, EnvironmentSendMessageParamsbody, RequestOptionsoptions?): EnvironmentSendMessageResponse`

**post** `/v1/environments/{connectionId}/messages`

Send a message to a specific environment connection

### Parameters

- `connectionID: string`

- `body: EnvironmentSendMessageParams`

  - `messages: Array<UnionMember0 | UnionMember1>`

    - `UnionMember0`

      - `client_message_id: string`

      - `content: string | Array<UnionMember1>`

        - `string`

        - `Array<UnionMember1>`

          - `text: string`

          - `type: "text"`

            - `"text"`

      - `role: "user"`

        - `"user"`

      - `otid?: string`

    - `UnionMember1`

      - `approvals: Array<UnionMember0 | UnionMember1>`

        - `UnionMember0`

          - `status: "success" | "error"`

            - `"success"`

            - `"error"`

          - `tool_call_id: string`

          - `tool_return: string | Array<UnionMember1>`

            - `string`

            - `Array<UnionMember1>`

              - `text: string`

              - `type: "text"`

                - `"text"`

          - `stderr?: Array<string> | null`

          - `stdout?: Array<string> | null`

          - `type?: "tool"`

            - `"tool"`

        - `UnionMember1`

          - `approve: boolean`

          - `tool_call_id: string`

          - `reason?: string | null`

          - `type?: "approval"`

            - `"approval"`

          - `updated_input?: Record<string, unknown> | null`

      - `type: "approval"`

        - `"approval"`

  - `agentId?: string`

  - `conversationId?: string | null`

### Returns

- `EnvironmentSendMessageResponse`

  - `message: string`

  - `success: boolean`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.environments.sendMessage('connectionId', {
  messages: [
    {
      client_message_id: 'client_message_id',
      content: 'string',
      role: 'user',
    },
  ],
});

console.log(response.message);
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

- `EnvironmentListResponse`

  - `connections: Array<Connection>`

    - `id: string`

    - `connectedAt: number | null`

    - `connectionId: string | null`

    - `connectionName: string`

    - `deviceId: string`

    - `firstSeenAt: number`

    - `lastHeartbeat: number | null`

    - `lastSeenAt: number`

    - `organizationId: string`

    - `podId: string | null`

    - `apiKeyOwner?: string`

    - `currentMode?: "default" | "standard" | "acceptEdits" | 2 more`

      - `"default"`

      - `"standard"`

      - `"acceptEdits"`

      - `"bypassPermissions"`

      - `"unrestricted"`

    - `metadata?: Metadata`

      - `gitBranch?: string`

      - `lettaCodeVersion?: string`

      - `nodeVersion?: string`

      - `os?: string`

      - `self_update?: SelfUpdate`

        - `supported: boolean`

        - `writable: boolean`

        - `install_path?: string`

        - `manual_command?: string`

        - `reason?: string`

      - `supported_commands?: Array<string>`

      - `workingDirectory?: string`

    - `userId?: string`

  - `hasNextPage: boolean`

### Environment Retrieve Response

- `EnvironmentRetrieveResponse`

  - `id: string`

  - `connectedAt: number | null`

  - `connectionId: string | null`

  - `connectionName: string`

  - `deviceId: string`

  - `firstSeenAt: number`

  - `lastHeartbeat: number | null`

  - `lastSeenAt: number`

  - `organizationId: string`

  - `podId: string | null`

  - `apiKeyOwner?: string`

  - `currentMode?: "default" | "standard" | "acceptEdits" | 2 more`

    - `"default"`

    - `"standard"`

    - `"acceptEdits"`

    - `"bypassPermissions"`

    - `"unrestricted"`

  - `metadata?: Metadata`

    - `gitBranch?: string`

    - `lettaCodeVersion?: string`

    - `nodeVersion?: string`

    - `os?: string`

    - `self_update?: SelfUpdate`

      - `supported: boolean`

      - `writable: boolean`

      - `install_path?: string`

      - `manual_command?: string`

      - `reason?: string`

    - `supported_commands?: Array<string>`

    - `workingDirectory?: string`

  - `userId?: string`

### Environment Send Message Response

- `EnvironmentSendMessageResponse`

  - `message: string`

  - `success: boolean`
