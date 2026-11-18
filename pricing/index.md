---
title: Pricing | Letta Docs
description: Pricing for Letta plans and credits
applies_to:
  backends:
    - cloud
  interfaces:
    - web
    - desktop
    - cli
    - sdk
---

## For individuals

You can get started with Letta for free by bringing your own API keys or an external coding plan, such as ChatGPT/Codex, Kimi, or Z.AI. Free plans are limited to 3 stateful agents.

Pro is $20/month and includes $20 in credits each month, which you can use on any model and for remote sandboxes. Pro also raises the limit to 20 stateful agents. Usage is shown in dollar amounts, and you can purchase additional credits at any time.

## For teams

You can share agents across your team (and set permissions for access) to create custom agents for your organization, and allow agents within your organization to communicate and collaborate.

Adding members to an organization requires Teams Pro, which includes everything in Pro plus shared agents and permissions.

## Plans

- [Individual](#tab-panel-4)
- [Teams / Enterprise](#tab-panel-5)

### Free

Get started at no cost.

$0 /month

- Up to 3 stateful agents
- 5 MiB of storage per memory repository
- Bring your own API keys and external coding plans
- Purchase credits for Letta-hosted models

[View quickstart ↗](/quickstart/index.md)

### Pro

Monthly credits for any model.

$20 /month

- $20/month in credits for any model
- Remote sandboxes, charged against credits
- Up to 20 stateful agents
- 50 MiB of storage per memory repository

[Get Pro ↗](https://chat.letta.com/preferences/usage)

### Teams Pro

Everything in Pro, for teams.

$20 /seat/month

- Everything in Pro
- Add teammates to your organization
- Share agents and set access control

[Get Teams Pro ↗](https://chat.letta.com/preferences/usage)

### Enterprise

For high volume enterprises

Custom

- Volume-based pricing
- Role-based access control
- SAML/OIDC SSO
- Dedicated support

[Contact us ↗](https://forms.letta.com/request-demo)

If you would like to configure managed per-seat pricing for your business, please [contact us](mailto:support@letta.com?subject=Letta%20Code%20Enterprise%20Pricing%20Inquiry).

### How much usage do I need?

Your ideal usage will vary depending on how you use your agents. Workloads that involve heavy tool use and token generation (e.g. coding or computer use tasks) spend credits faster.

- **Chat users**: Often stay within the $20 of included credits
- **Limited coding users**: May fit within the included credits depending on workloads
- **Casual coding users** (a few hours per day): Typically \~$100/mo+ usage
- **Power users** (long sessions, many parallel agents): Often approach or exceed $200+/mo in total usage

For agent power users (many hours of coding per day, or heavy automated use), we highly recommend combining the Letta Code CLI with an external coding plan, such as the [zAI coding plan](https://z.ai/subscribe), or [ChatGPT coding plan](https://chatgpt.com/codex/pricing/) (ChatGPT Plus/Pro).

---

## Frequently asked questions

Can I use my own API keys?

Yes. All plans support bringing your own API keys (BYOK). When you connect your own keys (via `/connect` in the Letta Code CLI), usage goes directly through your provider account instead of consuming Letta credits.

What are credits?

Credits are a standard cost unit for resources in Letta, such as LLM inference and CPU cycles. Model requests consume credits at a rate depending on model API pricing. For current model pricing, see [chat.letta.com/preferences/models](https://chat.letta.com/preferences/models).

How is tool execution charged?

Server-side tools on the Letta API incur a credit cost for CPU time, billed at $0.00015/sec. Remote MCP tools are executed by the MCP provider, so they do not have a credit cost. Letta built-in tools are free, with the exception of web search/fetch tools. Client-side tools, such as bash tools in the Letta Code CLI, run on your machine, so they do not incur a credit cost.

What are the usage limits for my plan?

The Free plan has no included model usage; bring your own API keys or an external coding plan, or purchase credits. Pro includes $20/month in credits, usable across any model and for sandboxes. Usage is shown in dollar amounts in the [usage dashboard](https://chat.letta.com/preferences/usage).

What happens when I reach my limit?

When your included credits run out, you can keep going by purchasing more credits or enabling auto top-up in the [usage dashboard](https://chat.letta.com/preferences/usage).

Where can I ask more questions?

Reach out to [support@letta.com](mailto:support@letta.com?subject=Letta%20Code%20Enterprise%20Pricing%20Inquiry), or join our community on [Discord](https://discord.gg/letta).
