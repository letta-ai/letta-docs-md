---
title: WhatsApp | Letta Docs
description: Connect WhatsApp to a Letta agent
---

WhatsApp sends through the linked WhatsApp account. Keep self-chat only enabled for personal numbers. Disable it only for a dedicated agent number, because replies will appear as that WhatsApp number.

## 1. Choose a WhatsApp account

Use a WhatsApp account you control. The default setup is **self-chat only**, which lets you talk to the agent by messaging yourself in WhatsApp and drops messages from other chats.

If you are using a dedicated WhatsApp number for the agent, you can disable self-chat only during setup. Letta Code will ask you to confirm that replies will appear under the linked WhatsApp number before continuing.

## 2. Configure

```
letta channels configure whatsapp
```

The interactive wizard will:

- Auto-install the WhatsApp runtime dependencies
- Ask whether to keep self-chat only enabled
- Let you choose a DM policy (`pairing`, `allowlist`, or `open`)
- Optionally bind the WhatsApp account to an agent for account-scoped routing
- Let you choose group behavior (`disabled`, `mention`, or `open`)
- Ask whether to download inbound media and transcribe voice memos when `OPENAI_API_KEY` is set

Config is written to `~/.letta/channels/whatsapp/accounts.json`.

## 3. Start the server with WhatsApp enabled

```
letta server --channels whatsapp
```

On first start, the listener prints a linked-device QR code. In WhatsApp, open **Settings > Linked Devices > Link a Device** and scan the QR code. Session state is stored under `~/.letta/channels/whatsapp/auth/`.

## 4. Pair or route a chat

For the default self-chat flow, message yourself in WhatsApp. With the default `pairing` DM policy, the chat receives a one-time pairing code. Complete the pairing from the CLI:

```
letta channels pair \
  --channel whatsapp \
  --code B5ZR5H \
  --agent <your-agent-id> \
  --conversation <your-conversation-id>
```

You can also pair from within an active agent session:

```
/channels whatsapp pair B5ZR5H
```

For a dedicated agent number with an account-bound agent, direct chats can route according to the configured DM policy. Group messages route only when group mode is `mention` or `open`; set `allowed_groups` to restrict which groups the agent can see.

## 5. Chat

Messages from WhatsApp now flow into the agent’s conversation. The `MessageChannel` tool supports sending messages, reacting to messages, and uploading files on WhatsApp. Inbound media is downloaded only when you enabled that option during setup.
