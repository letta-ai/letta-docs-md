---
title: Discord | Letta Docs
description: Connect Discord to a Letta agent
---

## 1. Create a Discord bot

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications) and click **New Application**
2. Open the **Bot** tab. Under **Privileged Gateway Intents**, enable **Message Content Intent**
3. Click **Reset Token** and copy the bot token (starts with `MT...` or similar)
4. Open the **OAuth2 > URL Generator** tab, select the `bot` scope, and grant the permissions your setup needs. Common permissions are Send Messages, Read Message History, Add Reactions, Create Public Threads, Send Messages in Threads, and Attach Files. Then open the generated URL to invite the bot to your server.

## 2. Configure

```
letta channels configure discord
```

The interactive wizard will:

- Auto-install the Discord runtime dependencies
- Ask for your bot token
- Let you choose a DM policy (`open`, `allowlist`, or `pairing`)
- Let you choose guild channel behavior (`mention-only` or `open`)
- Ask whether mentions should auto-create Discord threads
- Ask whether to enable inbound debounce, reaction acknowledgements, and audio transcription

Config is written to `~/.letta/channels/discord/accounts.json`.

## 3. Start the server with channels enabled

```
letta server --channels discord
```

You’ll see `[Discord] Bot started as YourBot#1234` in the output. The bot begins listening for guild messages and DMs immediately.

## 4. Bind the Discord bot to an agent

Like Slack, Discord binds the bot to a single agent (there’s no per-chat pairing):

```
letta channels bind --channel discord --agent <your-agent-id>
```

The `--agent` flag defaults to the `LETTA_AGENT_ID` env var. If you have multiple Discord bots configured, pass `--account-id` to specify which one.

You can also bind from the [Letta app](/platform/desktop-app/index.md) under **Connections > Discord**.

## 5. Chat

Once bound, DM the bot, `@mention` it in a channel, or send a message in a guild channel configured with `open` mode to start chatting.

**Discord routing behavior:**

- **@mentions in channels**: Each mention creates a new conversation for the agent. The agent replies in-thread, and subsequent messages in that thread are forwarded without requiring mentions.
- **Open guild channels**: Channels configured with `allowed_channels` mode `open` can route non-mention messages to the bound agent.
- **DMs**: Each DM gets a 1:1 mapping to a conversation. Routes are auto-created on first message.
- **DM policy**: Discord defaults to `pairing` (recommended) — unknown DMs receive a one-time code an operator must approve. `allowlist` and `open` are also supported.

## Restricting the bot to specific guild channels

By default, a Discord bot listens in every guild channel it can see. To narrow that down, set `allowed_channels`. DMs are unaffected.

`allowed_channels` supports two shapes:

- A legacy string array, where every listed channel runs in `mention-only` mode.
- A mode map, where each channel ID maps to `mention-only` or `open`.

`mention-only` means the bot responds when it is `@mentioned` in the channel, then continues inside the routed thread or conversation. `open` means the bot may process ambient non-mention messages in that channel. Use `open` carefully and only in channels where the bot should see every message.

Edit `~/.letta/channels/discord/accounts.json`:

```
{
  "accounts": [
    {
      "account_id": "...",
      "token": "...",
      "dm_policy": "pairing",
      "allowed_users": [],
      "allowed_channels": {
        "1234567890123456789": "mention-only",
        "9876543210987654321": "open"
      },
      "agent_id": "agent-..."
    }
  ]
}
```

You can also use the legacy array form when every allowed guild channel should stay mention-only:

```
{
  "allowed_channels": ["1234567890123456789", "9876543210987654321"]
}
```

Use `"*"` in the map as a wildcard default for visible guild channels:

```
{
  "allowed_channels": {
    "*": "mention-only",
    "9876543210987654321": "open"
  }
}
```

For thread messages, the Discord channel adapter checks the parent guild channel when available.

Or set allowed channels from the [Letta app](/platform/desktop-app/index.md) under **Connections > Discord > Manage > Bot settings > Allowed guild channels**.

To find a channel ID, enable Developer Mode in Discord (User Settings → Advanced), then right-click the channel and choose **Copy Channel ID**. Leave `allowed_channels` empty or unset to listen in every channel the bot can see.

## Advanced Discord options

The Discord account config also accepts these optional keys:

| Key                            | Behavior                                                                                                                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `default_permission_mode`      | Default permission mode for new Discord conversations. One of `standard`, `acceptEdits`, or `unrestricted`. Defaults to `standard`.                                          |
| `auto_thread_on_mention`       | Create a Discord thread when the bot is mentioned in a guild channel. New accounts default to `false`; older migrated accounts may keep their previous auto-thread behavior. |
| `thread_policy_by_channel`     | Per-channel overrides for auto-threading, for example `{ "123": true, "456": false }`.                                                                                       |
| `acknowledge_message_reaction` | Add lightweight reaction acknowledgements such as eyes/check marks around processing.                                                                                        |
| `inbound_debounce_ms`          | Debounce rapid open-channel messages. Values are capped at 10,000 ms.                                                                                                        |
| `transcribe_voice`             | Attempt to transcribe audio attachments when `OPENAI_API_KEY` is available.                                                                                                  |
| `remove_stale_routes`          | Allow route-cleanup flows to remove routes that no longer match `allowed_channels`; defaults to `false`.                                                                     |
