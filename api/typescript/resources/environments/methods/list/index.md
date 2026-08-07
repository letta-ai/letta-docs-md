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
