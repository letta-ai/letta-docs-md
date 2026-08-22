---
title: Slack | Letta Docs
description: Connect Slack to a Letta agent
---

If you’re using Letta-hosted agents, use the [native Slack integration](/platform/cloud-agents/slack/index.md) instead, which is always-on and does not require running an additional gateway server.

## 1. Create a Slack app

1. Go to [api.slack.com/apps](https://api.slack.com/apps) and click **Create New App**
2. Choose **From a manifest**, select your workspace, paste the JSON manifest below, and create the app
3. Generate an **app-level token**: go to **Settings > Basic Information**, scroll to **App-Level Tokens**, click **Generate Token and Scopes**, give it a name (e.g. “main”), add the `connections:write` scope, and click **Generate**. Copy the token (`xapp-...`).
4. **Install the app**: go to **Settings > Install App**, click **Install to Workspace**, authorize, then copy the **Bot User OAuth Token** (`xoxb-...`)

Slack app manifest

```
{
  "display_information": {
    "name": "Letta Code",
    "description": "Slack connector for Letta Code"
  },
  "features": {
    "bot_user": {
      "display_name": "Letta Code Slack Bot",
      "always_online": true
    },
    "app_home": {
      "messages_tab_enabled": true,
      "messages_tab_read_only_enabled": false
    }
  },
  "oauth_config": {
    "scopes": {
      "bot": [
        "app_mentions:read",
        "channels:history",
        "chat:write",
        "files:read",
        "files:write",
        "groups:history",
        "im:history",
        "reactions:read",
        "reactions:write",
        "users:read"
      ]
    }
  },
  "settings": {
    "org_deploy_enabled": false,
    "socket_mode_enabled": true,
    "is_hosted": false,
    "token_rotation_enabled": false,
    "event_subscriptions": {
      "bot_events": [
        "app_mention",
        "message.channels",
        "message.groups",
        "message.im",
        "reaction_added",
        "reaction_removed"
      ]
    }
  }
}
```

This manifest pre-configures Socket Mode, all required scopes, event subscriptions, and App Home messaging.

## 2. Configure

```
letta channels configure slack
```

The wizard asks for both tokens and your DM policy (`open` or `allowlist`).

If you choose `allowlist`, you’ll need Slack user IDs. To find a user ID: open the user’s profile in Slack, click the **three-dot menu** (⋯), and select **Copy member ID**. IDs start with `U` or `W`.

## 3. Start the server

```
letta server --channels slack
```

## 4. Bind the Slack app to an agent

Unlike Telegram (which uses pairing codes), Slack requires binding the app to an agent before any messages will route:

```
letta channels bind --channel slack --agent <your-agent-id>
```

The `--agent` flag defaults to the `LETTA_AGENT_ID` env var. If you have multiple Slack accounts configured, pass `--account-id` to specify which one.

You can also bind from the [Letta app](/platform/desktop-app/index.md) under **Connections > Slack**.

## 5. Chat

Once bound, DM the app or `@mention` it in a channel to start chatting.

**Slack routing behavior:**

- **@mentions in channels**: Each mention creates a new conversation for the agent. The agent replies in-thread, and all subsequent messages in that thread are forwarded without requiring mentions.
- **DMs**: Each DM chat gets a 1:1 mapping to a conversation. Routes are auto-created on first message.
- **DM policy**: Slack defaults to `open` (recommended). `allowlist` is also supported for DMs. The `pairing` policy does not apply to Slack.

## Advanced Slack options

The Slack account config also accepts these optional keys:

| Key                       | Behavior                                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `default_permission_mode` | Default permission mode for new Slack conversations. One of `standard`, `acceptEdits`, or `unrestricted`. Defaults to `unrestricted`. |
| `transcribe_voice`        | Attempt to transcribe audio attachments when `OPENAI_API_KEY` is available.                                                           |
| `show_completed_reaction` | Add a reaction when a request completes. Defaults to `true`.                                                                          |
| `listen_mode`             | When `true`, unmentioned Slack thread replies are delivered read-only until an `@mention`. Defaults to `false`.                       |
