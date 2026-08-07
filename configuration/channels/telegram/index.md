---
title: Telegram | Letta Docs
description: Connect Telegram to a Letta agent
---

## 1. Create a bot

Create a Telegram bot via [@BotFather](https://t.me/BotFather) and copy your bot token.

## 2. Configure

```
letta channels configure telegram
```

The interactive wizard will:

- Auto-install the Telegram runtime dependencies
- Ask for your bot token (validates it against the Telegram API)
- Let you choose a DM policy (`pairing`, `allowlist`, or `open`)

Config is written to `~/.letta/channels/telegram/accounts.json`.

## 3. Start the server with channels enabled

```
letta server --channels telegram
```

You’ll see `[Telegram] Bot started as @your_bot` in the output. The bot begins long-polling for messages immediately.

## 4. Pair a Telegram chat to an agent

Send any message to your bot from Telegram. With the default `pairing` policy, the bot replies with a pairing code and instructions to complete setup in the Letta app or CLI.

You can complete the pairing from the CLI:

```
letta channels pair \
  --channel telegram \
  --code B5ZR5H \
  --agent <your-agent-id> \
  --conversation <your-conversation-id>
```

The `--agent` flag defaults to the `LETTA_AGENT_ID` env var and `--conversation` defaults to `LETTA_CONVERSATION_ID` (or `"default"`).

You can also pair from within an active agent session (app, CLI, or desktop):

```
/channels telegram pair B5ZR5H
```

## 5. Chat

Messages from Telegram now flow into the agent’s conversation. The agent responds using the `MessageChannel` tool, which converts markdown to Telegram-safe HTML formatting (bold, italic, code, links, etc.).
