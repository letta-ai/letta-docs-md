---
title: Letta Agent SDK reference | Letta Docs
description: Client methods, session interface, and option types for the Letta Agent SDK
---

Use this reference after the [Quickstart](/agent-sdk/quickstart/index.md) when you need method names, session shape, or option interfaces.

### Client methods

| Method                                      | Description                                                                                         |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `client.createAgent(options?)`              | Create a new persistent agent                                                                       |
| `client.createSession(agentId, options?)`   | Start a new conversation on the specified agent                                                     |
| `client.resumeSession(id, options?)`        | Resume session (pass `agent-xxx` for default conversation, or `conv-xxx` for specific conversation) |
| `client.prompt(message, agentId, options?)` | One-shot convenience for scripts, smoke tests, and evals; applications should use sessions          |

### Client options

| Backend  | Required options | Common optional controls                                                               |
| -------- | ---------------- | -------------------------------------------------------------------------------------- |
| `local`  | None             | `appServer.requestTimeoutMs`, `appServer.startupTimeoutMs`, `appServer.harnessBackend` |
| `remote` | `url`            | `authToken`, `requestTimeoutMs`, `WebSocket`                                           |
| `cloud`  | None             | `apiKey`, `environment`, `sandbox`, `requestTimeoutMs`, `webSocketAuth`                |

`requestTimeoutMs` controls how long the SDK waits for a protocol response or turn. Browser and React Native applications should import the portable client from `@letta-ai/letta-agent-sdk/client`; see the [quickstart](/agent-sdk/quickstart#browser-and-react-native/index.md).

### Cloud repository client

`client.repositories` manages hosted repositories for clients configured with `backend: "cloud"`. Accessing this property on a local or remote client throws an error.

| Method                                                        | Returns                                 | Description                               |
| ------------------------------------------------------------- | --------------------------------------- | ----------------------------------------- |
| `client.repositories.create(params)`                          | `Promise<Repository>`                   | Create a hosted repository                |
| `client.repositories.list(params?)`                           | `Promise<ListRepositoriesResult>`       | List repositories using offset pagination |
| `client.repositories.get(repositoryId)`                       | `Promise<Repository>`                   | Get a repository by ID                    |
| `client.repositories.delete(repositoryId)`                    | `Promise<void>`                         | Delete a repository                       |
| `client.repositories.files.list(repositoryId, params?)`       | `Promise<ListRepositoryFilesResult>`    | List files and directories                |
| `client.repositories.files.create(repositoryId, params)`      | `Promise<RepositoryFileMutationResult>` | Create a text file                        |
| `client.repositories.files.read(repositoryId, params)`        | `Promise<RepositoryFile>`               | Read a file at the current or a given ref |
| `client.repositories.files.update(repositoryId, params)`      | `Promise<RepositoryFileMutationResult>` | Update content or rename a file           |
| `client.repositories.files.delete(repositoryId, params)`      | `Promise<DeleteRepositoryFileResult>`   | Delete a file                             |
| `client.repositories.versions.list(repositoryId, params?)`    | `Promise<RepositoryVersion[]>`          | List repository or file history           |
| `client.repositories.versions.get(repositoryId, sha, params)` | `Promise<RepositoryFile>`               | Read one file at a commit                 |

`client.agents.repositories` manages persistent links between repositories and Cloud agents:

- `list(agentId)` returns the repositories attached to an agent.
- `attach(agentId, repositoryId, options?)` attaches a repository until explicit removal.
- `detach(agentId, repositoryId, options?)` removes a persistent repository attachment.

See [Manage shared memory](/agent-sdk/repositories/index.md) for end-to-end examples and attachment lifecycle behavior.

### LettaCodeSession interface

Most applications use `send()`, `stream()`, and `close()`. Interactive clients can also restore conversation state, manage queued work, and reconcile device state after a reconnect.

#### Turns and history

| Method                           | Use                                                                        |
| -------------------------------- | -------------------------------------------------------------------------- |
| `send()`                         | Send a user message or add one to the active session queue                 |
| `stream()`                       | Consume assistant, reasoning, tool, queue, retry, error, and result events |
| `abort()`                        | Request cancellation without closing the session                           |
| `listMessages()`                 | Read paginated conversation history                                        |
| `listModels()` / `updateModel()` | Read or change the active model                                            |
| `sendCommand()`                  | Send a lower-level App Server protocol command                             |
| `close()`                        | Release the session and its local resources                                |

If the session connection closes unexpectedly during a turn, `stream()` emits an `error` followed by a failed `result`. The closed session cannot be reused. Call `resumeSession(conversationId)` to continue through a new session.

#### State, queues, and recovery

| Method                      | Use                                                                                                          |
| --------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `bootstrapState()`          | Fetch IDs, model, tools, initial history, and pending-approval state in one request                          |
| `recoverPendingApprovals()` | Replay an approval that was pending when the connection dropped                                              |
| `changeDeviceState()`       | Change the working directory or permission mode. Completion confirms transport only, not runtime application |
| `removeQueuedMessage()`     | Remove queued work and wait for the authoritative queue response                                             |
| `getDeviceStatus()`         | Request and wait for a fresh device-status snapshot                                                          |
| `onDeviceStatus()`          | Subscribe to device-status updates; returns an unsubscribe function                                          |

The session also exposes read-only `agentId`, `conversationId`, and `sessionId` values when the backend has resolved them.

Full TypeScript interface

```
interface LettaCodeSession {
  send(message: SendMessage): Promise<void>;
  stream(): AsyncGenerator<SDKMessage>;
  abort(): Promise<void>;
  close(): void;


  listMessages(options?: ListMessagesOptions): Promise<ListMessagesResult>;
  listModels(): Promise<ListModelsResult>;
  updateModel(update: string | UpdateModelOptions): Promise<UpdateModelResult>;
  sendCommand(command: SDKProtocolCommand): Promise<void>;
  sendCommand<TResponse extends SDKProtocolMessage = SDKProtocolMessage>(
    command: SDKProtocolCommand,
    options: SendCommandOptions,
  ): Promise<TResponse>;


  bootstrapState(
    options?: BootstrapStateOptions,
  ): Promise<BootstrapStateResult>;
  recoverPendingApprovals(
    options?: RecoverPendingApprovalsOptions,
  ): Promise<RecoverPendingApprovalsResult>;
  changeDeviceState(updates: ChangeDeviceStateOptions): Promise<void>;
  removeQueuedMessage(itemId: string): Promise<RemoveQueuedMessageResult>;
  getDeviceStatus(
    options?: GetDeviceStatusOptions,
  ): Promise<SessionDeviceStatus>;
  onDeviceStatus(listener: (status: SessionDeviceStatus) => void): () => void;


  readonly agentId: string | null;
  readonly conversationId: string | null;
  readonly sessionId: string | null;
}
```

#### History pagination

```
interface ListMessagesOptions {
  conversationId?: string;
  before?: string;
  after?: string;
  order?: "asc" | "desc";
  limit?: number;
}
```

### CreateAgentOptions

Options for `client.createAgent()` - these configure the persistent agent:

```
interface CreateAgentOptions {
  personality?: LettaCodePersonalityId;
  name?: string;
  description?: string;
  hidden?: boolean;
  tags?: string[];


  model?: string; // Defaults to the "auto" model preset
  embedding?: string;


  // Memory configuration (choose one approach)
  memory?: Array<
    string | { label: string; value: string } | { blockId: string }
  >;
  persona?: string;
  human?: string;
  memfs?: boolean; // Defaults to true


  // System prompt
  systemPrompt?:
    | string
    | SystemPromptPreset
    | { type: "preset"; preset: SystemPromptPreset; append?: string };


  // Tools and permissions
  baseTools?: string[]; // Defaults to web_search and fetch_webpage; [] attaches none
  allowedTools?: string[];
  disallowedTools?: string[];
  permissionMode?: "standard" | "acceptEdits" | "unrestricted" | "strict";
  canUseTool?: CanUseToolCallback;
  tools?: AnyAgentTool[];
  cwd?: string;


  // Runtime/harness controls available at creation
  skillSources?: SkillSource[];
  systemInfoReminder?: boolean;
}
```

The exported type includes some values that current creation backends reject. Use object memory blocks instead of memory preset names. Pass a custom `systemPrompt` string instead of a preset name or preset object. Configure `allowedTools` and `canUseTool` when you open the session. The current SDK does not support `disallowedTools` or `systemInfoReminder` as session overrides.

### CreateSessionOptions

`CreateSessionOptions` contains portable runtime controls. Client methods accept `LettaCodeClientSessionOptions`, which adds backend-specific execution options:

```
interface CreateSessionOptions {
  // Model configuration
  model?: string;
  reasoningEffort?: ReasoningEffort;


  // Tool restrictions
  allowedTools?: string[];
  toolset?: ClientToolsetConfig;
  permissionMode?: "standard" | "acceptEdits" | "unrestricted" | "strict";
  canUseTool?: CanUseToolCallback;
  tools?: AnyAgentTool[];
  mcpServers?: McpServers;


  // Runtime controls
  cwd?: string;
  skillSources?: SkillSource[]; // [] disables skills


  // Cloud repository resources
  resources?: RepositoryResource[];
}


interface LettaCodeClientSessionOptions extends CreateSessionOptions {
  environment?: LettaCodeEnvironment; // Cloud only
  sandbox?: LettaCodeCloudSandboxOptions; // Cloud only
  env?: Record<string, string>; // Local only; ignored elsewhere
  filesystemConfinement?: "memory"; // Local memory workers only
}
```

Supporting types:

```
type SkillSource = "bundled" | "global" | "agent" | "project";


interface ClientToolsetConfig {
  base?:
    | "auto"
    | "codex"
    | "codex_snake"
    | "default"
    | "gemini"
    | "gemini_snake"
    | "none";
  include?: string[];
}


type McpServers = Record<string, McpServerConfig>;


type McpServerConfig =
  | {
      type?: "stdio";
      command: string;
      args?: string[];
      env?: Record<string, string>;
      cwd?: string;
    }
  | {
      type: "http" | "sse";
      url: string;
      headers?: Record<string, string>;
    };


type LettaCodeEnvironment =
  | string
  | { name: string }
  | { id: string }
  | { connectionId: string }
  | { deviceId: string };


interface LettaCodeCloudSandboxOptions {
  ttlMinutes?: number; // Defaults to 5; valid range 1-60
  readyTimeoutMs?: number;
  readyPollIntervalMs?: number;
  refreshIntervalMs?: number;
  githubRepositories?: Array<{ owner: string; repo: string }>;
  terminateOnClose?: boolean; // Defaults to false
}
```

### Repository types

```
interface Repository {
  id: string;
  name: string;
  createdAt: string;
  updatedAt: string;
}


interface CreateRepositoryParams {
  name: string;
}


interface ListRepositoriesParams {
  limit?: number;
  offset?: number;
}


interface ListRepositoriesResult {
  repositories: Repository[];
  hasNextPage: boolean;
}


interface RepositoryResource {
  type: "repository";
  repositoryId: string;
  recompile?: boolean;
}


type AgentRepositoryPermissions = "read" | "read_write";
type AgentRepositoryRecompileTarget = "default" | false;


interface AgentRepository {
  id: string;
  name: string;
  isPrimary: boolean;
  permissions: AgentRepositoryPermissions;
}


interface AttachAgentRepositoryOptions {
  permissions?: AgentRepositoryPermissions;
  recompile?: AgentRepositoryRecompileTarget;
}


interface DetachAgentRepositoryOptions {
  recompile?: AgentRepositoryRecompileTarget;
}


interface RepositoryFileEntry {
  path: string;
  type: "file" | "directory";
}


interface ListRepositoryFilesParams {
  pathPrefix?: string;
  depth?: number;
  ref?: string;
}


interface ListRepositoryFilesResult {
  files: RepositoryFileEntry[];
  ref: string;
}


interface CreateRepositoryFileParams {
  path: string;
  content: string;
}


interface RepositoryFile {
  path: string;
  content: string;
  contentSha256: string;
  ref?: string;
}


interface UpdateRepositoryFileParams {
  path: string;
  content?: string;
  newPath?: string;
  precondition?: {
    contentSha256: string;
  };
}


interface RepositoryFileMutationResult {
  path: string;
  contentSha256: string;
  commitSha: string;
}


interface DeleteRepositoryFileParams {
  path: string;
}


interface DeleteRepositoryFileResult {
  success: boolean;
  commitSha: string;
}


interface RepositoryVersion {
  sha: string;
  message: string;
  timestamp: string;
  author_name: string | null;
}


interface ListRepositoryVersionsParams {
  path?: string;
  limit?: number;
}


interface GetRepositoryVersionParams {
  path: string;
}
```

`files.read()` accepts `{ path: string; ref?: string }`. All types above are exported from `@letta-ai/letta-agent-sdk`.
