---
title: Signal | Letta Docs
description: Connect Signal to a Letta agent
---

Signal support uses a local `signal-cli` bridge. Use a dedicated Signal number when possible. If you connect a personal number, enable `self_chat_mode` and talk to the agent through Signal’s Note to Self / self-chat.

## 1. Start a Signal bridge

The recommended runtime is native `signal-cli daemon`:

```
signal-cli -c ~/.local/share/signal-cli-letta daemon \
  --http 127.0.0.1:8080 \
  --receive-mode on-connection \
  --ignore-stories
```

Keep the daemon running while Letta is running. The Signal channel expects the runtime JSON-RPC/SSE endpoints at `/api/v1/check`, `/api/v1/rpc`, and `/api/v1/events`.

## 2. Configure

```
letta channels configure signal
```

The wizard can use native `signal-cli` commands for QR/device linking or SMS/voice registration. If Signal requires captcha, it will ask for the `signalcaptcha://...` URL from [signalcaptchas.org](https://signalcaptchas.org/).

Config is written to `~/.letta/channels/signal/accounts.json`.

## 3. Start the server with Signal enabled

```
letta server --channels signal
```

## 4. Pair or route a chat

With the recommended `pairing` DM policy, the first inbound Signal DM receives a one-time pairing code. Complete pairing from the CLI:

```
letta channels pair \
  --channel signal \
  --code B5ZR5H \
  --agent <your-agent-id> \
  --conversation <your-conversation-id>
```

You can also pair from an active agent session:

```
/channels signal pair B5ZR5H
```

For personal-number setups, keep `self_chat_mode` enabled. In self-chat mode, Letta only routes Note to Self/self-chat messages and rejects outbound sends to other recipients.
