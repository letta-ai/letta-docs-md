---
title: Letta Desktop | Letta Docs
description: Install chat.letta.com as a desktop app
applies_to:
  backends:
    - cloud
  interfaces:
    - web
    - desktop
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

## Local development

Unlike the legacy desktop app, the Letta desktop PWA app only works with signed in accounts (agents synced to Letta Cloud). To run agents with the local backend, where all agent state is stored on a local machine, use the [Letta CLI](/platform/cli/index.md), [Agent SDK](/agent-sdk/index.md), or create a custom UI on the [App Server](/self-hosting/app-server/index.md) (see our [mobile app](/agent-sdk/demo-apps/mobile/index.md) example as a reference).
