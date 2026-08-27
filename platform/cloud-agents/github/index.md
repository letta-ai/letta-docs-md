---
title: GitHub integration | Letta Docs
description: Give your cloud agents access to your GitHub repositories
---

Connect your GitHub org to Letta so that agents running on cloud computers can access your repositories to do work — sweeping bug reports, opening pull requests, or exploring your codebase.

![Asking a Letta agent to work on a GitHub repository from chat.letta.com](/images/cloud-agents-github.png)

## Setup

To sync your GitHub org to Letta, go to the [Integrations](https://chat.letta.com/preferences/integrations) page and connect your GitHub account. Once connected, agents in your Letta org running on cloud computers will be able to clone, read, and push to the repositories you grant access to.

## Usage

Mention a repository in your prompt (for example, `letta-ai/letta-code`) and the agent will pull it onto its cloud computer and get to work. Commits made to repos via the cloud sandbox will show up as made by the `letta-integration` GitHub app.
