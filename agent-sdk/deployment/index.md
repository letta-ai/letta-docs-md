---
title: Deploying your agents | Letta Docs
description: Deployment patterns and client setup options for the Letta Agent SDK
---

The Letta Agent SDK is the recommended application interface across managed, local, and self-hosted deployments. The selected backend determines which underlying API or runtime transport the SDK manages for you.

| Goal                                                       | SDK configuration                  | Execution environment | Where agent state lives              |
| ---------------------------------------------------------- | ---------------------------------- | --------------------- | ------------------------------------ |
| Fully managed agent and execution environment              | `backend: "cloud"`                 | Managed sandbox       | Letta Cloud                          |
| Bring your own machine                                     | `backend: "cloud"` with `computer` | Selected computer     | Letta Cloud                          |
| Keep agent state and the execution environment fully local | `backend: "local"`                 | Current machine       | Current machine                      |
| Connect to a runtime you operate                           | `backend: "remote"`                | App Server machine    | Determined by the App Server backend |

## Letta Cloud

Use `backend: "cloud"` to host agents in Letta Cloud and run tools in managed cloud environments.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


const agentId = await client.createAgent({
  persona:
    "You are a digital operations partner who can research, write reports, coordinate tasks, and remember durable context.",
});


await using session = client.resumeSession(agentId);
```

### Managed sandboxes

If you do not pass a `computer`, the SDK creates a managed sandbox for the session. The sandbox is where tools run; the agent’s memory and conversation state remain hosted in Letta Cloud.

By default, the SDK waits for the sandbox to come online and refreshes it while the session is active. When the session closes, the sandbox remains available until its TTL expires so reconnecting clients and other sessions can continue using it.

Configure those options on the client:

```
const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
  sandbox: {
    ttlMinutes: 5,
    readyTimeoutMs: 120_000,
    readyPollIntervalMs: 1_000,
    refreshIntervalMs: 240_000,
    terminateOnClose: false,
  },
});
```

`ttlMinutes` controls the requested sandbox TTL on refresh. `readyTimeoutMs` and `readyPollIntervalMs` control startup waiting. `refreshIntervalMs` controls background refresh while the session is open. `terminateOnClose` defaults to `false`; set it to `true` only when the session exclusively owns the sandbox and should request best-effort eager cleanup.

If you pass `cwd`, use a path inside the sandbox. Local paths like `process.cwd()` are not mounted into managed sandboxes automatically.

#### Recover from an expired sandbox

If Letta Cloud reaps a conversation-scoped sandbox before the next refresh, `send()` throws `CloudManagedSandboxExpiredError` before transmitting the turn. Close the old SDK session, resume the same conversation to create a fresh sandbox, and retry once:

```
import {
  CloudManagedSandboxExpiredError,
  LettaAgentClient,
} from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});
const conversationId = "conv-abc123";
let session = client.resumeSession(conversationId);


async function sendWithSandboxRecovery(message: string): Promise<void> {
  for (let attempt = 0; attempt < 2; attempt += 1) {
    try {
      await session.send(message);
      for await (const event of session.stream()) {
        if (event.type === "assistant") process.stdout.write(event.content);
      }
      return;
    } catch (error) {
      if (!(error instanceof CloudManagedSandboxExpiredError) || attempt > 0) {
        throw error;
      }
      session.close();
      session = client.resumeSession(conversationId);
    }
  }
}
```

Only retry automatically for this pre-send expiration error. If a connection fails after `send()` succeeds, inspect the conversation history before retrying because the original message may already have reached the runtime.

### Bring your own machine

Use a [computer you control](/platform/computers/byom/index.md) to provide an agent hosted in Letta Cloud with an execution environment on your own machine. The machine connects outward to Letta Cloud and remains available to its hosted clients.

```
const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
  computer: { name: "work-laptop" },
});
```

You can also select the computer per session:

```
await using session = client.resumeSession(agentId, {
  computer: { deviceId: "device-..." },
  cwd: "/workspace/project",
});
```

`computer` accepts a name or selector object:

```
type ComputerSelector =
  | string
  | { name: string }
  | { id: string }
  | { connectionId: string }
  | { deviceId: string };
```

Use `deviceId` or a computer `id` to save a selection across reconnects. Use `connectionId` only for the current live connection. Discover available computers with `client.computers.list({ onlineOnly: true })`.

`computer` and `sandbox` are mutually exclusive. Use `computer` when you choose the runtime; omit it when the SDK should create a managed sandbox. The older `environment` option is deprecated in favor of `computer`.

## Local App Server

Use `backend: "local"` for a fully local deployment. The Agent SDK package includes Letta Code and starts an SDK-owned App Server subprocess on the current machine.

```
const client = new LettaAgentClient({ backend: "local" });


const agentId = await client.createAgent({
  persona:
    "You are a resident engineering teammate for this repository. You inspect files, learn conventions, and keep durable memory of important patterns.",
});


await using session = client.resumeSession(agentId, {
  cwd: "/Users/me/project",
});
```

Agent state, filesystem access, and tool execution remain on the current machine. The SDK owns the App Server lifecycle, so your application does not need to start or connect to the server manually.

## Self-hosted App Server

Use `backend: "remote"` when the agent runtime should run on a machine you operate separately from your application.

For a fully self-hosted runtime, start App Server with the local backend:

Terminal window

```
letta server --backend local --listen ws://127.0.0.1:4500
```

Then connect the SDK:

```
const client = new LettaAgentClient({
  backend: "remote",
  url: "http://127.0.0.1:4500",
  requestTimeoutMs: 120_000,
});
```

`requestTimeoutMs` controls how long the SDK waits for an App Server protocol response or turn before timing out. Loopback listeners are unauthenticated by default. For remote access, enable App Server authentication and pass its token as `authToken`.

With `--backend local`, agent state and the execution environment remain on the App Server machine. App Server can also run with `--backend cloud`; in that configuration, agent state is hosted in Letta Cloud while the execution environment remains on the App Server machine.

Unlike a computer connected to Letta Cloud, App Server accepts a direct connection from your application. It does not register itself as a selectable computer in Letta Cloud’s hosted clients.

For container deployment, see [Self-hosting](/self-hosting#deployment/index.md). For startup, authentication, and lower-level protocol details, see [App Server](/platform/app-server/index.md).

## What to read next

- [Quickstart](/agent-sdk/quickstart/index.md) — working code for each backend
- [Sessions, turns, and durability](/agent-sdk/sessions/index.md) — what persists across connections
- [Creating agents](/agent-sdk/agents/index.md) — per-backend MemFS locations
- [App Server](/platform/app-server/index.md) — startup, authentication, and protocol details
