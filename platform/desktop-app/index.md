---
title: Letta app | Letta Docs
description: Use the Letta app on macOS, Windows, or Linux
---

The Letta app is your personal command center for your stateful agents. Everything about an agent is visible in one place: you can chat with it, and view and edit its memory, schedules, channels, and skills.

Your agents aren’t tied to your desktop, either. The same agent can run on your local machine or on other computers — a [cloud sandbox](/platform/computers/cloud-sandboxes/index.md), a workstation, or a [remote VM](/platform/computers/byom/index.md) — keeping its memory and context wherever it runs.

![Chatting with an agent in the Letta app](/images/desktop/chat-agent.png)

## Getting started

[  macOS Apple Silicon ](https://download.letta.com/mac/dmg/arm64)[  Windows x64 ](https://download.letta.com/windows/nsis/x64)[  Windows ARM64 ](https://download.letta.com/windows/nsis/arm64)[  Linux AppImage, x64 ](https://download.letta.com/linux/appImage/x64)[  Linux AppImage, ARM64](https://download.letta.com/linux/appImage/arm64)

Once installed, follow the [quickstart](/quickstart/index.md) to connect model providers and send your first message.

## Choosing a computer

Your agent can run on any computer connected to your Letta account, keeping the same memory and context wherever it goes. Use the environment picker in the message composer to switch between your local machine, a [cloud sandbox](/platform/computers/cloud-sandboxes/index.md), or any [connected remote computer](/platform/computers/byom/index.md), such as a workstation or cloud VM.

![Selecting a computer from the environment picker](/images/desktop/select-computer.png)

## Connecting model providers

Open **Connect model providers** from the bottom-left menu to add [models](/configuration/models/index.md) to your agent. You can connect API keys for providers like OpenAI, Anthropic, Google Gemini, and OpenRouter, or sign in with a coding plan subscription.

![Connecting model providers in the Letta app preferences](/images/desktop/adding-models.png)

## View and edit files

The built-in file viewer lets you browse the working directory on the selected computer, and view and edit the files your agent is working with. Both markdown and HTML files can be viewed fully rendered or as source.

![Viewing a rendered markdown file in the Letta app](/images/desktop/render-file.png)

## Configure channels

Use the **Channels** page to connect your agent to [external messaging channels](/configuration/channels/index.md) like Telegram, Slack, Discord, and WhatsApp. Each channel can be toggled on or off, configured with its own management permissions, and opened directly as a conversation.

![Configuring Slack and Discord channels in the Letta app](/images/desktop/channel-config.png)

Every message your agent sends and receives through a channel is visible in the app: channel conversations appear in the sidebar alongside your direct chats, so you can follow along as your agent responds on other platforms — including multi-user threads.

![A Discord thread with multiple users in the Letta app](/images/desktop/discord-multi-user.png)

## Run schedules

Use the **Schedules** page to set up [one-time or recurring prompts](/configuration/schedules/index.md) for your agent, like a morning briefing or an hourly email triage. When creating a schedule, you can choose which computer and conversation the scheduled prompt runs in.

![Creating a schedule in the Letta app](/images/desktop/create-schedule.png)

Selecting a schedule shows its status, run history, and details. You can also trigger a scheduled task immediately with **Send now**.

![Viewing and running a schedule in the Letta app](/images/desktop/view-and-run-schedule.png)

## Memory

Use the **Memory** page to explore and edit your agent’s [memory](/configuration/memory/index.md). The graph view shows how your agent’s memory files reference each other, and selecting a node lets you view, edit, and save its contents directly.

![Editing an agent's persona memory in the graph view](/images/desktop/memory-editing.png)

## Skills

Use the **Skills** page to browse available skills, attach skills to an agent, and add new skills.

![Browsing and attaching skills in the Letta app](/images/desktop/skills.png)

To import a skill from GitHub:

1. Click **Add skill**.
2. Choose **Import from GitHub**.
3. Paste a GitHub URL to a skill directory containing `SKILL.md`.
4. Click **Import**.

The import flow validates the URL, clones the repository, verifies the skill, and installs it globally on your machine. You can also choose **Create with agent** from the same **Add skill** menu when you want your agent to create a new skill for a repeated workflow.
