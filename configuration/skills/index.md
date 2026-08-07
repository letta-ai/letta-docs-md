---
title: Skills | Letta Docs
description: Create and use reusable skills to extend your agent's capabilities
---

The Letta agent harness implements the open [Agent Skills](https://agentskills.io) standard. Skills are portable across the Letta app and CLI, Codex, Claude Code, Hermes Agent, OpenClaw, and other compatible agents.

Skills are directories containing instructions and resources that your agent can load when relevant. Think of them as reusable capability packages for specialized tasks — API integrations, testing workflows, deployment procedures.

Skills can include executable scripts in addition to instructions and reference files. A skill can call an external API directly, use an SDK, or connect to an MCP server by having the agent run its bundled scripts with the tools available on the selected computer. API access follows the agent’s [permissions](/configuration/permissions/index.md); store credentials as [secrets](/configuration/secrets/index.md) instead of putting them in the skill.

In most agents, skills are “device-bound” - they are stored on the machine the agent is running on, so if your agent moves machines, it loses the skills. In the Letta app and CLI, agents can write skills into their own memory systems, so that skills persist with the agent as part of its identity.

## Skill scopes

Agents are able to use skills from the current project (project-scoped skills), their own memory (agent-scoped skills), and skills provided automatically by the Letta harness (bundled skills). Letta automatically registers skills from the current project (`.agents/skills`), current computer (`~/.letta/skills`), and current agent.

```
flowchart TD
    subgraph Project["Project-scoped"]
        P[".agents/skills/"]
    end

    subgraph AgentScope["Agent-scoped (MemFS)"]
        A["$MEMORY_DIR/skills/"]
    end

    subgraph Bundled["Computer-scoped"]
        G["~/.letta/skills/"]
    end

    P --> Skills["Current agent skills"]
    A --> Skills
    G --> Skills
```

| Location                  | Scope    | Description                                                                                            |
| ------------------------- | -------- | ------------------------------------------------------------------------------------------------------ |
| `${MEMORY_DIR}/skills/`   | Agent    | Persistent skills specific to one Letta agent, stored inside that agent’s git-backed memory filesystem |
| `.agents/skills/`         | Project  | Primary project-local location for interactive client-side skills                                      |
| `~/.letta/skills/`        | Computer | Skills shared across all Letta agents running on this machine                                          |
| (bundled with Letta Code) | Built-in | Skills that ship with Letta Code (always available to any Letta agent)                                 |

### Agent-scoped skills

Letta agents have skills that are part of their identity, that they manage over time. Agent-scoped skills are cloned to whatever computer the agent is currently working on, so are always available regardless of where the agent is running or what project it is working on. Use agent-scoped skills for memory or workflows specific to your agent.

### Project-scoped skills

Project-scoped skills are your standard skills in the local directory at `.agents/skills`. Project-scoped skills are specific to that project, and typically managed in the project’s repository (e.g. GitHub). These skills are *not* managed by Letta, and belong to the project not the agent. Use project-scoped skills for project-specific information or workflows.

### Computer-scoped skills

You can also install skills globally for a computer by placing skills in `~/.letta/skills`. Only use this skill directory for skills required for any agents running on that computer.

### Bundled skills

The Letta harness bundles built-in skills for capabilities such as memory management, search, mods, self-configuration, and cross-agent communication.

## Installing new skills

The easiest way to install a skill is to simply **ask your agent to install it**. For example, to install the [frontend design](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design/skills/frontend-design) skill from Anthropic’s example skills repo (which teaches your agent how to build pretty websites), you can simply ask Letta Code:

```
> Can you install the following skill? https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design/skills/frontend-design
```

You can also install skills from the Letta app:

1. Open the **Skills** page.
2. Click **Add skill**.
3. Choose **Import from GitHub**.
4. Paste a GitHub URL that points to a skill directory containing `SKILL.md`.
5. Click **Import**.

The desktop app validates the URL, clones the repository, verifies the skill, and installs it globally on your machine. You can then attach that skill to an agent from the Skills page.

To install directly into an agent’s MemFS from the CLI, use:

Terminal window

```
letta install <skill-source> --agent <agent-id>
letta skills list --agent <agent-id>
letta skills delete <skill-name> --agent <agent-id>
```

`<skill-source>` can be a GitHub skill directory, a Hermes-style `official/...` skill, or a ClawHub `clawhub/...` or `clawhub:<slug>` skill.

You can also manually install skills by copying the folder to one of the supported skills folders that Letta Code reads from (see below).

### Where can I find new skills?

Start by browsing (or ask your agent to browse) the [Letta](https://github.com/letta-ai/skills) and [Anthropic](https://github.com/anthropics/skills/tree/main/skills) skills repos. A few recommend skills include:

- [Letta API client](https://github.com/letta-ai/skills/tree/main/letta/letta-api-client): become an expert at building apps on the Letta API
- [Frontend design](https://github.com/anthropics/skills/tree/main/skills/frontend-design): build beautiful websites with consistent styles
- [Slack GIF creator](https://github.com/anthropics/skills/tree/main/skills/slack-gif-creator): teach your agent to build Slack GIFs
- [PDF skill](https://github.com/anthropics/skills/tree/main/skills/pdf): tools for parsing PDF documents
- [Powerpoint (.pptx) skill](https://github.com/anthropics/skills/tree/main/skills/pptx): tools for editing .pptx files
- [Excel (.xlsx) skill](https://github.com/anthropics/skills/tree/main/skills/xlsx): tools for editing Excel files
- [Remotion skill](https://github.com/remotion-dev/skills/tree/main/skills/remotion): teach your agent how to make product videos using the Remotion React video editor

Only download skills from trusted sources. Skills can contain malware and dangerous prompts that trick your agent into leaking your data.

## Invoking skills directly

Letta Code automatically decides when to load a relevant skill, but you can also invoke one explicitly from the prompt with slash syntax:

Terminal window

```
/<skill-name> [optional instructions]
```

For example:

Terminal window

```
/acquiring-skills find and install a skill for browser testing
```

Direct invocation is useful when you already know which skill should guide the work. Letta Code loads the skill’s instructions into the conversation, then continues with the rest of your request.

Use `/skills` to browse available skills by source before invoking one by name.

## Creating new skills

You may want to create new skills to capture important reusable behaviors. For example, while working on your project, there may be certain sequences of actions taken by developers (e.g. a database migration) that is best represented to the agent as a *skill* to be used by many agents, rather than a memory.

Letta agents have a built-in “skill creator” skill, so you can simply prompt your agent to create a new skill:

```
> Can we turn the database migration we just did into a project-scoped skill?
```

For creating skills by hand, refer to the official [Agent Skills](https://agentskills.io) documentation.

Letta Code also ships a built-in `letta-help` skill. The Tutor personality uses it for guided onboarding, and you can invoke it directly when you want a walkthrough of memory, delegation, tools, skills, search, subagents, or schedules:

Terminal window

```
/letta-help help me get started
```
