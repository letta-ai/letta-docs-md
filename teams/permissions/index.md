---
title: Configuring permissions | Letta Docs
description: Control who can access agents and conversations in your organization
---

Joining an organization does not give a collaborator access to every agent and conversation. Letta combines organization roles with sharing controls so teammates can collaborate without making all agent activity visible to the entire organization.

## Organization roles

Each organization member has a role that grants a set of organization-wide permissions:

- **Admin** members can manage the organization and its members. They can also access all agents and conversations in the organization.
- **Editor** members can create and manage resources, but only see their own agents and conversations plus agents shared with the organization.
- **Analyst** members have read and messaging access, subject to the same agent and conversation visibility rules.

Invited collaborators join as Editors by default. An Admin can change a member’s role from the members page in [organization settings](https://platform.letta.com/settings/organization).

## Agent access

Agents are private to their creator by default. Other collaborators cannot discover or open the agent unless either:

- The creator shares the agent with the organization.
- Their role grants permission to manage all agents.

To share an agent, open its settings, select **Share agent**, and change access from **Only me** to **Anyone in your organization**. Organization members can then discover the agent and chat with it. You can return the setting to **Only me** to remove that shared access.

## Conversation access

Conversations are private to the collaborator who created them by default. Members without permission to manage all conversations can only list and open their own conversations, including when several collaborators use the same shared agent.

Sharing an agent lets teammates start their own conversations with it. It does not make your existing conversations visible to them. Organization Admins can access all conversations.

## Tool permissions

Agent access and tool permissions are separate. Sharing an agent does not automatically allow every tool call on every connected computer. Each computer still applies its own approval rules when the agent uses local tools.

See [Permissions](/configuration/permissions/index.md) for local permission modes, approval rules, and project settings. See [Secrets](/configuration/secrets/index.md) for managing credentials used by shell commands and tools.
