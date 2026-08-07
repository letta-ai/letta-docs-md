---
title: Custom channels | Letta Docs
description: Build a custom messaging channel for Letta agents
---

Custom channels let you connect a Letta agent to a messaging platform that is not bundled with the Letta CLI. A custom channel runs as a local adapter under `~/.letta/channels/<channel-id>/`, receives inbound messages from your platform, routes them to an agent conversation, and lets the agent reply through the `MessageChannel` tool.

Channels are different from skills. A skill gives an agent a reusable capability or action set, such as how to read from or post to a service. A channel is the communication medium itself: the delivery surface for inbound messages, outbound replies, account routing, and chat pairing. For example, a Slack skill might describe how to use Slack-related tools, while a Slack channel is the live messaging connection that receives Slack messages and sends replies.

Custom channels are headless. They participate in routing, pairing, and `MessageChannel`, but they do not get custom setup screens in the Letta app. If a channel needs a first-party setup UI, Slack/Discord-style auto-routing, rich protocol-specific account snapshots, or compatibility migrations, it should be built as a bundled channel instead.

## When to use a custom channel

Use a custom channel for:

- Community integrations, experiments, and internal workflows
- Platforms that can be managed with local config files
- Channels that can use generic pairing or route files
- Headless deployments where operators are comfortable editing JSON/YAML

Do not use a custom channel to override a bundled channel. The Letta CLI ignores custom channel IDs that collide with first-party channels such as `telegram`, `slack`, `discord`, `whatsapp`, and `signal`. Use a distinct ID like `matrix-community`, `signal-test`, or `custom-chat`.

## Directory layout

Create a directory for your channel under `~/.letta/channels/`:

```
~/.letta/channels/
  matrix-community/
    channel.json
    plugin.mjs
    accounts.json
    routing.yaml
    pairing.yaml
    runtime/
      package.json
      node_modules/
```

The required files are:

| File            | Purpose                                                           |
| --------------- | ----------------------------------------------------------------- |
| `channel.json`  | Registers the channel and declares runtime dependencies           |
| `plugin.mjs`    | Exports the channel adapter and optional `MessageChannel` actions |
| `accounts.json` | Stores account records and channel-owned config                   |

`routing.yaml`, `pairing.yaml`, and `runtime/` are created or updated by the channel runtime and CLI commands.

## Create `channel.json`

`channel.json` tells the Letta CLI how to load your channel adapter:

```
{
  "id": "matrix-community",
  "displayName": "Matrix Community",
  "entry": "./plugin.mjs",
  "runtimePackages": ["matrix-js-sdk@34.10.0"],
  "runtimeModules": ["matrix-js-sdk"]
}
```

Rules:

- `id` must match the directory name.
- `id` can contain lowercase letters, numbers, underscores, and hyphens.
- `entry` is resolved relative to the channel directory.
- `runtimePackages` are installed into the channel’s `runtime/` directory by `letta channels install <channel-id>`.
- `runtimeModules` are resolved from bundled first-party runtimes first, then from the channel’s local `runtime/` directory.

The adapter is implemented as a local module, but the product concept is still a channel: a communication surface with account config, inbound delivery, and outbound replies.

## Create `accounts.json`

Each channel account uses the shared channel account envelope. The `config` object belongs to your channel adapter and may contain secrets or platform-specific settings:

```
{
  "accounts": [
    {
      "channel": "matrix-community",
      "accountId": "main",
      "displayName": "Matrix Community",
      "enabled": true,
      "dmPolicy": "pairing",
      "allowedUsers": [],
      "config": {
        "homeserverUrl": "https://matrix.example.com",
        "accessToken": "...",
        "roomId": "!room:matrix.example.com"
      },
      "createdAt": "2026-01-01T00:00:00.000Z",
      "updatedAt": "2026-01-01T00:00:00.000Z"
    }
  ]
}
```

DM policies control who can message your agent:

| Policy      | Behavior                                                                                                          |
| ----------- | ----------------------------------------------------------------------------------------------------------------- |
| `pairing`   | Unknown users receive a one-time code. An operator approves the code and binds the chat to an agent conversation. |
| `allowlist` | Only users listed in `allowedUsers` can message the channel.                                                      |
| `open`      | Any user can message, but a route must exist unless your adapter creates routes through custom logic.             |

Start with `pairing` while testing. Use `allowlist` or `open` only when you understand the deployment and audience.

## Create `plugin.mjs`

`plugin.mjs` exports either `channelPlugin` or `default`. This local module creates a channel adapter for each account.

```
export const channelPlugin = {
  metadata: {
    id: "matrix-community",
    displayName: "Matrix Community",
    runtimePackages: ["matrix-js-sdk@34.10.0"],
    runtimeModules: ["matrix-js-sdk"],
  },


  async createAdapter(account) {
    return {
      id: `matrix-community:${account.accountId}`,
      channelId: "matrix-community",
      accountId: account.accountId,
      name: account.displayName ?? "Matrix Community",


      async start() {
        // Connect to the platform SDK and begin receiving messages.
      },


      async stop() {
        // Close sockets, polling loops, or SDK clients.
      },


      isRunning() {
        return true;
      },


      async sendMessage(message) {
        // Send message.text to message.chatId using your platform SDK.
        return { messageId: crypto.randomUUID() };
      },


      async sendDirectReply(chatId, text) {
        await this.sendMessage({ chatId, text });
      },


      onMessage: undefined,
    };
  },


  messageActions: {
    describeMessageTool() {
      return { actions: ["send"] };
    },


    async handleAction({ adapter, request, formatText }) {
      const formatted = formatText(request.message ?? "");
      const result = await adapter.sendMessage({
        channel: request.channel,
        chatId: request.chatId,
        text: formatted.text,
        parseMode: formatted.parseMode,
        threadId: request.threadId,
      });


      return `Message sent to ${request.channel} (message_id: ${result.messageId})`;
    },
  },
};
```

Implement `messageActions` for every channel where agents should reply. Without it, inbound messages can still reach the agent, but the `MessageChannel` tool will not know how to send outbound responses through your adapter.

## Deliver inbound messages

After your adapter connects to the external platform, call `adapter.onMessage(message)` when a platform message arrives.

A minimal inbound message includes the platform chat, sender, and text:

```
await adapter.onMessage?.({
  channel: "matrix-community",
  accountId: account.accountId,
  chatId: platformChatId,
  senderId: platformUserId,
  senderName: platformDisplayName,
  text: incomingText,
  messageId: platformMessageId,
  timestamp: new Date().toISOString(),
});
```

The channel runtime then:

1. Checks the account’s DM policy and allowlist.
2. Looks for an existing route in `routing.yaml`.
3. Creates or updates a pairing in `pairing.yaml` when approval is required.
4. Delivers routed messages to the bound agent conversation.
5. Exposes `MessageChannel` for conversations with an active route and running adapter.

## Install runtime dependencies

If your plugin declares runtime packages, install them before starting the server:

```
letta channels install matrix-community
```

For headless deployments, you can install runtimes as the server starts:

```
letta server --channels matrix-community --install-channel-runtimes
```

Runtime dependencies should resolve from the channel runtime directory, not from parent project or development `node_modules` folders. This keeps custom channels portable across machines.

## Start the channel

Run the Letta CLI with your channel enabled:

```
letta server --channels matrix-community
```

You can enable multiple channels with a comma-separated list:

```
letta server --channels telegram,matrix-community
```

## Pair or route a chat

With `dmPolicy` set to `pairing`, the first inbound message from an unknown user creates a pairing code. Approve that code from the CLI:

```
letta channels pair \
  --channel matrix-community \
  --code B5ZR5H \
  --agent <your-agent-id> \
  --conversation <your-conversation-id>
```

You can also add a route manually:

```
letta channels route add \
  --channel matrix-community \
  --account-id main \
  --chat-id <platform-chat-id> \
  --agent <your-agent-id> \
  --conversation default
```

Routes are stored in `~/.letta/channels/<channel-id>/routing.yaml`.

The standalone `letta channels pair` and `letta channels route add` commands update local state files. If the listener or server is already running, prefer the live Channels controls in the app/ADE for pairing and route updates, or restart the listener after changing routes from the CLI so the running adapter observes the new state.

## Test the full loop

Before sharing a channel, test all four legs:

1. Channel discovery and import: `letta channels status` should show your channel and account.
2. Inbound delivery: a platform message should call `adapter.onMessage(...)` and create a route or pairing.
3. Agent routing: after pairing or routing, the inbound message should appear in the target agent conversation.
4. Outbound response: an agent `MessageChannel` call should invoke `messageActions.handleAction(...)`, then `adapter.sendMessage(...)`.

If messages arrive but replies fail, check that `messageActions` is present and that `handleAction` passes the formatted message through your platform SDK.

## Security notes

- Store platform secrets in `accounts.json` under `config`; do not hard-code them in `plugin.mjs`.
- Keep `accounts.json` out of git if it contains real credentials.
- For public or shared channels, avoid exposing tool approval prompts to untrusted chats unless you have verified operator routing. Public approval prompts can leak tool inputs and invite forged approvals.
- Prefer `pairing` or `allowlist` while developing.

## Related docs

- [Channels](/configuration/channels/index.md)
- [Headless mode](/platform/cli/headless/index.md)
- [CLI reference](/platform/cli/reference/index.md)
