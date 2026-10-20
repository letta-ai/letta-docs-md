---
title: Letta Desktop | Letta Docs
description: Install chat.letta.com as a desktop app
applies_to:
  backends:
    - cloud
    - local
  interfaces:
    - web
    - desktop
    - cli
---

Letta Desktop is [chat.letta.com](https://chat.letta.com) installed as a desktop app. It opens in its own window, with its own dock or taskbar icon, and launches like any other app. Under the hood, it is a progressive web app (PWA), so it stays up to date with the web app.

## Install

### Chrome or Edge

1. Open [chat.letta.com](https://chat.letta.com).
2. Click the install icon at the right of the address bar. In Chrome you can also choose **More** (⋮) > **Cast, save, and share** > **Install page as app**; in Edge, choose **Settings and more** (…) > **More tools** > **Apps** > **Install this site as an app**.
3. Click **Install**.

If Letta Desktop is already installed, Chrome shows **Open in app** in the address bar when you visit chat.letta.com. Click it to switch to the app window.

### Safari on macOS

Requires macOS Sonoma 14 or later.

1. Open [chat.letta.com](https://chat.letta.com) in Safari.
2. Choose **File** > **Add to Dock**, or click the Share button and choose **Add to Dock**.
3. Click **Add**.

### Firefox

Firefox can install web apps only on Windows (Firefox 143 or later). On macOS or Linux, use Chrome, Edge, or Safari.

## Keep using your local agents

The previous Letta Code Desktop app was deprecated on October 12, 2026 and no longer runs. Your local agents still exist: Desktop and the [Letta CLI](/platform/cli/index.md) share `~/.letta/lc-local-backend` by default.

Install the CLI, then run `letta --backend local` and use `/agents` to pick an existing local agent. To resume it directly, run `letta --agent agent-local-<id>` with its full agent ID (also available in the `/agents` list).

The desktop PWA requires a signed-in Letta Cloud account. For local agents, use the CLI, [Agent SDK](/agent-sdk/index.md), or a custom UI on the [App Server](/self-hosting/app-server/index.md).
