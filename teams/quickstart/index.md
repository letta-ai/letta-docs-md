---
title: Get started | Letta Docs
description: Set up a Letta team for your organization
---

Letta for teams adds shared organizations, member management, and centralized billing.

Users in a team can shared agents and memory with each other. By default, agents that users create are private.

## Creating a team

Create a team by following these steps:

1. **Sign up for a Teams plan**

   To set up a Teams plan, follow these steps:

   1. Go to the [Usage](https://chat.letta.com/preferences/usage) page
   2. Click `Upgrade Plan` and select `Teams Plans`
   3. Complete the payment flow to set up the plan

2. **Invite users**

   Once you have a Teams plan, go to the [Members](https://chat.letta.com/preferences/organization/members) page to invite your teammates via email. See [Adding collaborators](/teams/collaborators/index.md) for more details on invitations and sharing agents.

3. **Add seats**

   By default, users you add will be on `Free` seats, which means they will be unable to use Letta-hosted models for inference.

   Click the `Manage seat` button in the [Members](https://chat.letta.com/preferences/organization/members) page to purchase `Pro` seats for members of your team to give them model access. Alternatively, configure your own BYOK providers in the [Models](https://chat.letta.com/preferences/models) page.

4. **Configure GitHub (optional)**

   If your team uses GitHub, sync your GitHub org to Letta on the [Integrations](https://chat.letta.com/preferences/integrations) page. By configuring your GitHub, agents in your Letta org running on cloud computers will be able to access your GitHub repos to do work.

5. **Configure Slack (optional)**

   You can easily bring your Letta agents to Slack with Letta’s native Slack integration. Simply visit an agent that you want to connect to Slack on [chat.letta.com](https://chat.letta.com), then click the `Connections` tab to configure a Slack app for that agent.

## FAQ

### ”Can other people on my team see my agents or conversations?”

No - by default, agents are private and are only visible to their creator and organization admins. If you would like to share your agents with other members of your team, simply navigate to your agent on [chat.letta.com](https://chat.letta.com), click the triple-dot next to your agents name, and click `Sharing settings`.

### ”How can I add my company’s own LLM gateway?”

Yes - if your LLM gateway is an OpenAI-compatible endpoint, you simply need to register a custom OpenAI provider in Letta Cloud. Go to the [model providers](https://chat.letta.com/preferences/models) page, click `Add`, then select the `OpenAI-compatible` provider type. You’ll need to have your custom endpoints API key and base URL to complete the setup.

If you have issues registering your OpenAI-compatible endpoint, please reach out to support for assistance.

### ”Can I add my own ChatGPT / Codex / zAI / etc plans?”

Yes - all standard BYOK model providers are supported on Letta Teams plans. Some OAuth-specific providers (such as ChatGPT plans) may need to be configured via the desktop app or CLI.

If you have issues configuring BYOK providers, please reach out to support for assistance.
