---
title: Automatic reply relay | Letta Docs
description: Send finalized assistant replies to a channel without MessageChannel calls
applies_to:
  backends:
    - local
  interfaces:
    - cli
    - sdk
---

Channel accounts default to `tool` mode: the agent must call `MessageChannel` to reply. Opt into `relay` to send each finalized assistant message automatically to its routed destination.

These instructions cover [local-backend Channels](/self-hosting/channels/index.md), not the [hosted Slack integration](/platform/cloud-agents/slack/index.md). Relay is on Letta Code main after [PR 4043](https://github.com/letta-ai/letta-code/pull/4043), but is not included in v0.34.1.

## Enable relay

Add `"reply_mode": "relay"` to an existing account in `~/.letta/channels/<channel>/accounts.json`. Keep its actual account ID, credential fields, and secret references. This excerpt shows only the relevant fields:

\~/.letta/channels/telegram/accounts.json (excerpt)

```
{
  "accounts": [
    {
      "account_id": "<existing-account-id>",
      "reply_mode": "relay"
    }
  ]
}
```

Restart the channel server after editing the file. Set `reply_mode` to `tool` to restore explicit replies; missing or invalid stored values also use `tool`.

An [App Server](/self-hosting/app-server/index.md) controller can update a running account instead:

```
{
  "type": "channel_account_update",
  "request_id": "update-reply-mode",
  "channel_id": "telegram",
  "account_id": "<existing-account-id>",
  "patch": { "reply_mode": "relay" }
}
```

There is no reply-mode CLI flag or settings toggle yet. Changes affect newly submitted inputs; active and queued inputs keep their captured policy.

## What changes

- Relay sends finalized messages in order, including messages before and after tools or approvals. It does not stream unfinished text, and errors or cancellation do not forward the unfinished current message.
- Relay ignores reasoning and subagent output and suppresses text already sent explicitly in the same turn.
- A single-destination relay input has no `MessageChannel` tool. Use `tool` mode for reactions, files, and proactive sends.
- An input with multiple or ambiguous destinations falls back to explicit replies through `MessageChannel`. Relay never broadcasts to several destinations.
- Queued channel inputs run as separate turns, even in the same chat, so one input cannot inherit another’s reply tools or destination.

The on-device gateway implements relay delivery. Remote gateway hosts must provide the relay transport and capture the per-input reply policy.
