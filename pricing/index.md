---
title: Pricing | Letta Docs
description: Pricing for the Letta app, CLI, and developer usage
---

## For Individuals

You can get started with Letta for free by using models with BYOK, including coding plans from ChatGPT/Codex, Kimi, and Z.AI. Free plans are limited to 3 stateful agents.

With the Pro plan, you can run agents in remote sandboxes, access usage quota for Letta Auto, and purchase credits to use across models (including for image generation).

## For Teams

You can share agents across your team (and set permissions for access) to create custom agents for your organization, and allow agents within your organization to communicate and collaborate.

Adding members to organization requires a Teams Pro account, which includes all the features of the individual Pro plan in addition to allowing shared resources.

## For Developers

Developer plans are usage-based for teams building on the Letta API with API keys and automated workloads. With a developer plan, you can create an unlimited number of agents but pay usage-based pricing.

## Plans

- [Personal Plans](#tab-panel-5)
- [Developer Plans](#tab-panel-6)
- [Teams / Enterprise](#tab-panel-7)

### Free

Get started at no cost.

$0 /month

- Limited agents
- Limited usage of Letta Auto
- Bring your own API keys and external coding plans

[View quickstart ↗](/quickstart/index.md)

### Pro

For personal use.

$20 /month

- Letta Auto weekly + monthly quota
- Pay-as-you-go overage
- Up to 20 stateful agents

[Get Pro ↗](https://platform.letta.com/settings/organization/usage)

Pricing on the Letta API Platform is usage-based. LLM usage is charged based on the underlying token costs of the model used.

### API Plan

For teams building on the Letta API.

$20 /month

- Unlimited agents
- $0.10 / active agent / mo
- $0.00015 / sec tool execution
- API key authentication
- Pay-as-you-go LLM usage

[Get started ↗](https://platform.letta.com/settings/organization/usage)

### Teams Pro

For teams

$20 /seat/month

- Add teammates to your organization
- Letta Auto weekly + monthly quota
- Share agents and set access control

[Get Teams Pro ↗](https://platform.letta.com/settings/organization/usage)

### Enterprise

For high volume enterprises

Custom

- Volume-based pricing
- Increased quotas
- Role-based access control
- SAML/OIDC SSO
- Dedicated support

[Contact us ↗](https://forms.letta.com/request-demo)

If you would like to configure managed per-seat pricing for your business, please [contact us](mailto:support@letta.com?subject=Letta%20Code%20Enterprise%20Pricing%20Inquiry).

### What is Letta Auto?

**Letta Auto** selects frontier models that balance general intelligence, coding knowledge, and speed. To use Letta Auto, select `Auto` in the model selector, or choose one of the more specialized routes for specific applications: `Auto Chat` for non-coding workloads, or `Auto Fast` for a model that’s optimized for additional speed over intelligence.

### How much usage do I need?

Your ideal plan will vary depending on how you use your agents. Workloads that involve heavy tool use and token generation (e.g. coding or computer use tasks) will drain quota faster.

- **Chat users**: Often stay within the Pro tier limits
- **Limited coding users**: May fit within Pro depending on workloads
- **Casual coding users** (a few hours per day): Typically \~$100/mo+ usage
- **Power users** (long sessions, many parallel agents): Often approach or exceed $200+/mo in total usage

For agent power users (many hours of coding per day, or heavy automated use), we highly recommend combining the Letta app or CLI with an external coding plan, such as the [zAI coding plan](https://z.ai/subscribe), or [ChatGPT coding plan](https://chatgpt.com/codex/pricing/) (ChatGPT Plus/Pro).

### What happens when I reach my Letta Auto limit?

When you exceed your included weekly or monthly usage, you can continue at pay-as-you-go API rates, available through purchasing credits. You can upgrade your plan, add credits, and configure auto-top up in your account’s [usage dashboard](https://platform.letta.com/settings/organization/usage).

---

## Frequently asked questions

Can I use my own API keys?

Yes. All plans support bringing your own API keys (BYOK). When you connect your own keys (via `/connect` in the Letta CLI), usage goes directly through your provider account instead of consuming Letta credits.

What’s the difference between Personal Plans and Developer Plans?

Personal Plans are for individual, hands-on use via the Letta app, CLI, or web app. They provide usage quotas that reset monthly. Personal Plan quotas require OAuth authentication through the Letta app, CLI, or web app.

Developer Plans are for developers and teams building applications on top of the Letta API with automated workloads. They use API key authentication with purely usage-based credit pricing.

Can I use a Developer Plan with the Letta app or CLI?

Yes. You can use a Developer Plan with the Letta app or CLI; usage will draw down credits from your balance.

We recommend most Letta app and CLI users choose Personal Plans. Personal Plans include Letta Auto quota and can enable auto top-up or additional usage when quota is exceeded.

What are credits?

Credits are a standard cost unit for resources in Letta, such as LLM inference and CPU cycles. Model requests consume credits at a rate depending on model API pricing. For current model pricing, see [platform.letta.com/models](https://platform.letta.com/models).

How is tool execution charged?

Server-side tools on the Letta API incur a credit cost for CPU time. On the API Plan, tool execution is billed at $0.00015/sec. Remote MCP tools are executed by the MCP provider, so they do not have a credit cost. Letta built-in tools are free, with the exception of web search/fetch tools. Client-side tools, such as bash tools in the Letta CLI, run on your machine, so they do not incur a credit cost.

What are the usage limits for my plan?

The free tier includes a limited number of total agents and LLM requests with rotating free models. Personal Plans include monthly usage quotas that scale with each tier. Developer Plans are pay-as-you-go and can be managed from your usage dashboard.

Paid plan users can view current usage in the [account dashboard](https://platform.letta.com/settings/organization/usage).

What happens when I reach my limit?

On Personal Plans, you can continue using Letta with pay-as-you-go pricing for additional models or overage. On Developer Plans, all usage is pay-as-you-go; you’ll be notified by email when approaching your spending limit.

Where can I ask more questions?

Reach out to [support@letta.com](mailto:support@letta.com?subject=Letta%20Code%20Enterprise%20Pricing%20Inquiry), or join our community on [Discord](https://discord.gg/letta).
