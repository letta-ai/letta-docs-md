---
title: Channels | Letta Docs
description: Connect external messaging platforms to your Letta agents
---

If you’re using Letta-hosted agents, use the [native Slack integration](/platform/cloud-agents/slack/index.md) instead, which is always-on and does not require running an additional gateway server.

Channels let your Letta agent receive and respond to messages from external platforms like Telegram, Slack, Discord, WhatsApp, and Signal. Messages from the platform flow into the agent’s conversation, and the agent replies using the `MessageChannel` tool.

## Getting started

You can set up channels via the [Letta app](/platform/desktop-app/index.md) or the CLI. The app provides a visual setup flow in the **Channels** sidebar tab. For CLI setup, choose a channel-specific guide:

- [Slack](/configuration/channels/slack/index.md)
- [Telegram](/configuration/channels/telegram/index.md)
- [Discord](/configuration/channels/discord/index.md)
- [WhatsApp](/configuration/channels/whatsapp/index.md)
- [Signal](/configuration/channels/signal/index.md)
- [Custom channels](/configuration/channels/custom/index.md)

## Channel slash commands

After a chat is connected, you can send these slash commands as normal messages in the Telegram, Slack, Discord, WhatsApp, or Signal chat. They are handled by the channel runtime before the message reaches the agent.

| Command       | Description                                                   |
| ------------- | ------------------------------------------------------------- |
| `/help`       | Show channel usage guidance                                   |
| `/status`     | Show account, listener, route, agent, and conversation state  |
| `/whoami`     | Show your access scope, tier, and runnable commands           |
| `/pause`      | Pause agent replies for the current routed chat               |
| `/resume`     | Resume agent replies for the current routed chat              |
| `/cancel`     | Cancel the in-progress agent turn for the current routed chat |
| `/chat`       | Show the Letta web chat link for the current route            |
| `/reflection` | Start a memory reflection pass for the current routed chat    |
| `/reflect`    | Alias for `/reflection`                                       |

For Slack threads, send the command in the routed thread when there may be more than one Letta thread in the same channel. Slack-native slash command payloads currently exist only for `/cancel`; the other commands are typed as regular chat messages.

## Architecture

```
flowchart LR
    subgraph Platform["Messaging platform"]
        TG["Telegram / Slack / Discord / WhatsApp / Signal"]
    end

    subgraph Local["Your machine (letta server)"]
        Adapter["Channel adapter<br/>(long-polling / Socket Mode / gateway)"]
        Registry["Channel registry"]
        Queue["Message queue"]
        Agent["Agent"]
        Tool["MessageChannel tool"]
    end

    TG -->|"Inbound message"| Adapter
    Adapter --> Registry
    Registry -->|"XML-wrapped message"| Queue
    Queue --> Agent
    Agent -->|"Tool call"| Tool
    Tool -->|"Outbound reply"| TG
```

1. The **adapter** receives messages from the platform (Telegram uses long-polling, Slack uses Socket Mode, Discord uses the gateway WebSocket, WhatsApp uses a linked-device WebSocket session, and Signal uses a local `signal-cli` bridge)
2. The **registry** checks sender access (DM policy, group policy, allowlists), looks up the route, and formats the message as XML
3. The message enters the agent’s **queue** as a `channel` source item
4. The agent processes it and calls the **MessageChannel** tool to reply
5. The tool converts markdown to platform-safe formatting and sends through the adapter

## Access control

Sender access is decided centrally on every inbound message — direct messages and group/channel messages, on every channel — before slash commands, approval replies, or routing run.

### DM policies

Each channel account has a DM policy that controls who can message the bot directly:

| Policy                                                          | Behavior                                                                                                                                                                        |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pairing` (default for Telegram, Discord, WhatsApp, and Signal) | Unknown users receive a one-time pairing code. An operator must approve the code to bind the chat to an agent.                                                                  |
| `allowlist`                                                     | Only allowed senders can message. Others are rejected.                                                                                                                          |
| `open` (default for Slack)                                      | Anyone can message. For Telegram, requires a route to exist. For Slack, Discord, WhatsApp, and Signal, routes are auto-created when the channel/account routing mode allows it. |

A sender is “allowed” if they appear in the account’s `allowed_users`, its `admin_users`, an [environment variable allowlist](#environment-variable-allowlists), or have completed pairing — these grants are a union. Allowlisted senders skip the pairing handshake, and paired senders stay allowed everywhere. A `"*"` entry in `allowed_users` allows everyone. WhatsApp and Signal entries are matched with identity normalization, so a phone number entry matches the platform’s internal sender ID forms.

Until pairing completes, senders under the `pairing` policy can only run the read-only commands `/help`, `/status`, and `/whoami`.

Defaults differ by channel. Telegram, Discord, WhatsApp, and Signal default to `pairing` (explicit approval per chat). Slack defaults to `open` (anyone can DM or mention the app, routes auto-provision); the `pairing` policy does not apply to Slack and behaves as `open`. WhatsApp also has self-chat and group-mode gates that can be stricter than the DM policy.

### Group sender policy

By default any participant of a group/channel the bot listens in can talk to the agent. Set `group_policy` on the account to restrict group senders:

| Value              | Behavior                                                                                       |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| `"open"` (default) | Any group participant can message the agent.                                                   |
| `"allowlist"`      | Only allowed senders (see above) can message the agent in groups; others are silently dropped. |

This composes with the existing chat-level gates (`allowed_channels` on Discord, `allowed_groups` on WhatsApp/Signal, `group_mode` mention gating): those decide **which chats** the bot listens in, while `group_policy` decides **which senders** inside those chats may talk to it.

### Admin command tiers

By default every allowed user can run every [channel slash command](#channel-slash-commands). To restrict operational commands, set `admin_users` on the account (or an admin environment variable). When at least one admin is configured:

- **Admins** can run every command.
- **Other users** can only run the read-only floor — `/help`, `/status`, `/whoami` — plus anything listed in `user_allowed_commands`.

If no admin is configured, command gating is disabled and behavior is unchanged. Admin entries are matched with the same identity normalization as allowlists, and `user_allowed_commands` accepts aliases (e.g. `reflect` for `/reflection`). Use `/whoami` in a chat to see your tier and the commands available to you.

\~/.letta/channels/discord/accounts.json (excerpt)

```
{
  "dm_policy": "allowlist",
  "allowed_users": ["1234567890"],
  "group_policy": "allowlist",
  "admin_users": ["9876543210"],
  "user_allowed_commands": ["cancel", "model"]
}
```

### Environment variable allowlists

Allowlists and admin lists can also be supplied via environment variables (comma-separated user IDs). They merge with the per-account configuration:

| Variable                                                                 | Description                                               |
| ------------------------------------------------------------------------ | --------------------------------------------------------- |
| `LETTA_CHANNELS_ALLOWED_USERS`                                           | Global allowlist applied to every channel                 |
| `LETTA_<CHANNEL>_ALLOWED_USERS` (e.g. `LETTA_TELEGRAM_ALLOWED_USERS`)    | Per-channel allowlist                                     |
| `LETTA_CHANNELS_ADMIN_USERS` / `LETTA_<CHANNEL>_ADMIN_USERS`             | Global / per-channel admin lists (activate command tiers) |
| `LETTA_CHANNELS_ALLOW_ALL_USERS=1` / `LETTA_<CHANNEL>_ALLOW_ALL_USERS=1` | Explicit opt-out of sender gating                         |

Once an allowed-users environment variable is configured, it restricts **every scope** on the affected channels — DMs and groups, including channels whose DM policy is `open`. Senders not covered by any grant are denied.

## Routing

Routes bind a platform chat ID to an agent + conversation pair. They’re stored in `~/.letta/channels/<channel>/routing.yaml`.

Routes are created automatically when pairing completes, or manually via the CLI:

```
# Add a route manually
letta channels route add \
  --channel telegram \
  --chat-id 123456789 \
  --agent agent-abc123 \
  --conversation default


# List all routes
letta channels route list


# List routes for a specific channel
letta channels route list --channel telegram


# Remove a route
letta channels route remove --channel telegram --chat-id 123456789
```

## CLI reference

| Command                                      | Description                                                                           |
| -------------------------------------------- | ------------------------------------------------------------------------------------- |
| `letta channels install <channel>`           | Install channel runtime dependencies (optional — `configure` does this automatically) |
| `letta channels configure <channel>`         | Interactive setup wizard (installs runtime deps if needed)                            |
| `letta channels status`                      | Show config, routing, and pairing state (JSON)                                        |
| `letta channels route list [--channel <ch>]` | Show routing table                                                                    |
| `letta channels route add [options]`         | Add a route binding a chat to an agent                                                |
| `letta channels route remove [options]`      | Remove a route                                                                        |
| `letta channels bind [options]`              | Bind a Slack or Discord channel account to an agent                                   |
| `letta channels pair [options]`              | Complete a pairing code and bind to agent (Telegram, WhatsApp, or Signal)             |

### Common flags

| Flag                  | Commands               | Description                                                                                          |
| --------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------- |
| `--channel <name>`    | route, pair, bind      | Channel name (`telegram`, `slack`, `discord`, `whatsapp`, `signal`)                                  |
| `--account-id <id>`   | route add/remove, pair | Account ID (required when multiple accounts exist for a channel, auto-resolved when only one exists) |
| `--chat-id <id>`      | route add/remove       | Platform chat/conversation ID                                                                        |
| `--agent <id>`        | route add, pair, bind  | Agent ID (defaults to `LETTA_AGENT_ID`)                                                              |
| `--conversation <id>` | route add, pair        | Conversation ID (defaults to `LETTA_CONVERSATION_ID` or `"default"`)                                 |
| `--code <code>`       | pair                   | Pairing code from the bot                                                                            |

## Headless deployment

For server/Docker deployments without interactive setup:

1. Pre-write the config files to `~/.letta/channels/<channel>/`
2. Start with the `--install-channel-runtimes` flag to auto-install dependencies:

```
letta server --channels telegram --install-channel-runtimes
```

Or install runtimes separately:

```
letta channels install telegram
```

### Environment variables

| Variable                | Description                                          |
| ----------------------- | ---------------------------------------------------- |
| `LETTA_AGENT_ID`        | Default agent ID for `pair` and `route add` commands |
| `LETTA_CONVERSATION_ID` | Default conversation ID (fallback: `"default"`)      |
| `LETTA_API_KEY`         | API key for `letta server` authentication            |

Access-control allowlists can also be configured via environment variables — see [Environment variable allowlists](#environment-variable-allowlists).

## State files

| File                                   | Description                                                                                        |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `~/.letta/channels/<ch>/accounts.json` | Channel account configuration (tokens, DM/group policy, allowlists, admin tiers, account metadata) |
| `~/.letta/channels/<ch>/routing.yaml`  | Route table (chat ID to agent/conversation binding)                                                |
| `~/.letta/channels/<ch>/pairing.yaml`  | Pending and approved pairings                                                                      |

## Connection lifecycle

Channels integrate with the `letta server` WebSocket connection:

- On **connect**: channel adapters register their message handler and flush any buffered messages
- On **disconnect**: adapters pause delivery but keep polling/listening. Messages buffer until reconnection.
- On **shutdown**: adapters stop cleanly

This means if `letta server` briefly loses its WebSocket connection, no Telegram, Slack, Discord, WhatsApp, or Signal messages are dropped — they buffer and deliver when the connection restores.

You can also configure channels on [remote devices](/platform/computers/byom/index.md) — simply swap the selected device in the Connections menu of the Letta app.
