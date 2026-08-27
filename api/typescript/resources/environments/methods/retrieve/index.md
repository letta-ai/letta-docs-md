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
