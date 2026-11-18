---
title: Subagents | Letta Docs
description: Specialized agents for task decomposition and parallel execution
applies_to:
  backends:
    - cloud
    - local
  interfaces:
    - web
    - desktop
    - cli
    - sdk
---

Subagents are specialized agents that your main agent can spawn to handle complex tasks autonomously. By delegating work to focused subagents, your main agent can keep its context window clean and make use of parallelism to divide and conquer tasks.

The Letta Code harness includes [built-in subagents](#built-in-subagents) optimized for common workflows, and you can [create custom subagents](#creating-custom-subagents) for specialized tasks.

## How it works

Your main agent launches subagents with the `Agent` tool. By default, a new subagent forks the main agent’s conversation, so it starts with full context. Set `fork_context: false` to start one with only the prompt.

The subagent runs autonomously with its own system prompt, tools, and model. The final message from the subagent is returned to the main agent, which keeps the main agent’s context clean.

For example, if the main agent wants to understand where a certain function is located in the codebase, it can launch a subagent to search. That subagent may use hundreds of thousands of tokens to read hundreds of files, but the main agent will only see the final answer - saving the main agent from unnecessary context “pollution” from tool calls and returns.

### Background subagents

Subagents run in the background: the `Agent` tool returns a receipt with a task ID right away, and the main agent continues its own work while the subagent runs.

When the subagent finishes, a completion notification is automatically injected into the conversation, and the main agent can read the result.

### Ephemeral conversations

On Letta Cloud, a fresh subagent that does not fork the main agent’s conversation runs as an ephemeral conversation linked to the main agent, rather than as a separate agent. It uses the main agent’s MCP servers and secrets, and its receipt carries a conversation ID instead of a new agent ID. Subagents on the local backend or on another computer still run as their own agent.

- **Follow up:** the main agent calls `SendAgentMessage` with the subagent’s conversation ID to steer it while it works or send it a new task.
- **Reply to the main agent:** a subagent calls `SendAgentMessage` without an agent or conversation ID to message the agent that launched it. Its final report reaches the main agent automatically.
- **Stop:** the main agent calls `TaskStop` with the subagent’s task ID.

### Launching stateful agents as subagents

It is also possible to deploy an arbitrary Letta agent as a subagent by specifying its `agent_id`. This lets your main agent invoke other agents—with their own rich memories, personalities, and skillsets—as subagents that can read, write, and edit code.

To deploy an existing agent as a subagent, your main agent simply needs to know its agent ID (both agents must exist in the same Letta API org/project):

```
> I have another agent that's an expert at web design. Can you ask them to review your changes? Their agent ID is ...
```

If you don’t remember their agent ID, your main agent can also use the built-in [“finding agents” skill](/configuration/skills/index.md) to find them:

```
> Can you ask my other agent "Dora Designer" to review this PR as a subagent? I forgot their agent ID though.
```

## Built-in subagents

Subagents without a configured model inherit the main agent’s model. When launching without a preset, the main agent can set `model` (for example, `Spawn a subagent with Opus`).

`recall` is the only built-in preset the main agent can select with `subagent_type`; [custom subagents](#creating-custom-subagents) can be selected the same way. The harness launches `init` and `reflection` itself.

| Subagent     | Purpose                                                                | Access     |
| ------------ | ---------------------------------------------------------------------- | ---------- |
| `recall`     | Search conversation history for past discussions and decisions         | Read-only  |
| `init`       | Fast initialization of agent memory from the current project           | Read/write |
| `reflection` | Background “sleep-time” memory consolidation from recent conversations | Read/write |

## Creating custom subagents

Create custom subagents by adding Markdown files with YAML frontmatter to the `.letta/agents/` directory.

### File structure

```
.letta/
└── agents/
    └── my-subagent.md
```

You can also create global subagents at `~/.letta/agents/` that are available across all projects.

### Subagent file format

Example subagent file:

.letta/agents/security-reviewer.md

```
---
name: security-reviewer
description: Reviews code for security vulnerabilities and suggests fixes
tools: Glob, Grep, Read
model: sonnet
memoryBlocks: human, persona
---


You are a security code reviewer.


## Instructions


- Search for common vulnerability patterns (SQL injection, XSS, etc.)
- Check authentication and authorization code
- Review input validation
- Identify hardcoded secrets or credentials


## Output Format


1. List of findings with severity (critical/high/medium/low)
2. File paths and line numbers for each issue
3. Recommended fixes
```

### Frontmatter fields

| Field          | Required | Description                                                                                      |
| -------------- | -------- | ------------------------------------------------------------------------------------------------ |
| `name`         | Yes      | Unique identifier (lowercase, hyphens allowed). Must start with a letter.                        |
| `description`  | Yes      | When to use this subagent (shown in the `Agent` tool and /subagents)                             |
| `tools`        | No       | Comma-separated list of allowed tools, or `all`. Defaults to `all`.                              |
| `model`        | No       | Model to use (e.g., `haiku`, `sonnet`, `opus`). Defaults to inheriting from main agent.          |
| `memoryBlocks` | No       | Which memory blocks the subagent can access: specific list, `all`, or `none`. Defaults to `all`. |
| `skills`       | No       | Comma-separated list of skills to auto-load                                                      |

### Model and toolset behavior

For the main interactive agent, switching models with `/model` can automatically switch toolsets (see [Models and Toolsets](/configuration/models/index.md)).

For subagents, `model` and `tools` are configured independently:

- `model` selects which model the subagent runs on.
- `tools` defines which tools the subagent is allowed to use.

Changing a subagent’s `model` does not automatically change its configured tools.

### System prompt

The body of the Markdown file (after the frontmatter) becomes the subagent’s system prompt. Write clear instructions for what the subagent should do and how it should format its output.

### Override priority

Custom subagents override built-ins with the same name. Project-level subagents (`.letta/agents/`) override global ones (`~/.letta/agents/`).

### Access levels

When creating a subagent from a preset, `subagent_type` selects the preset, which sets its tools, model, and read/write scope; other launch options are ignored. To deploy an existing agent, pass its `agent_id` and omit `subagent_type`.
