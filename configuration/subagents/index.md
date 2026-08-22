---
title: Subagents | Letta Docs
description: Specialized agents for task decomposition and parallel execution
---

Subagents are specialized agents that your main agent can spawn to handle complex tasks autonomously. By delegating work to focused subagents, your main agent can keep its context window clean and make use of parallelism to divide and conquer tasks.

The Letta agent harness includes [seven built-in subagent types](#built-in-subagents) optimized for common workflows, and you can [create custom subagents](#creating-custom-subagents) for specialized tasks.

## How it works

Your main agent can launch subagents using a specialized subagent tool. When the subagent tool is called, the Letta agent harness launches a new subagent in a subprocess.

The subagent runs autonomously with its own system prompt, tools, and model. The final message from the subagent is returned to the main agent, which keeps the main agent’s context clean.

For example, if the main agent wants to understand where a certain function is located in the codebase, it can launch a `general-purpose` subagent to search. That subagent may use hundreds of thousands of tokens to read hundreds of files, but the main agent will only see the final answer - saving the main agent from unnecessary context “pollution” from tool calls and returns.

### Background subagents

By default, launching a subagent blocks: the subagent tool does not return until the subagent finishes. Background subagents flip this around: the main agent can call subagents in “background mode”, and the main agent is free to continue its own work while the subagent runs.

When the subagent finishes, a completion notification is automatically injected into the conversation, and the main agent can read the result.

### Launching stateful agents as subagents

By default, the built-in subagents are not reused - they are created fresh on each invocation.

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

Each subagent has a recommended model, but the Letta agent harness now resolves built-in subagents to `auto` or `auto-fast` by default when available. You can still override the model with prompting (for example, `Spawn a recall agent with Opus`).

| Subagent           | Purpose                                                                | Recommended model | Access     |
| ------------------ | ---------------------------------------------------------------------- | ----------------- | ---------- |
| `fork`             | Fork the parent conversation with full context and tools               | `inherit`         | Read/write |
| `general-purpose`  | Full implementation - research, plan, and make changes                 | `auto`            | Read/write |
| `history-analyzer` | Migrate conversation history from Claude Code or Codex into memory     | `auto`            | Read/write |
| `init`             | Fast initialization of agent memory from the current project           | `auto-fast`       | Read/write |
| `memory`           | Reorganize memory blocks into a cleaner hierarchy with less redundancy | `auto`            | Read/write |
| `recall`           | Search conversation history for past discussions and decisions         | `auto-fast`       | Read-only  |
| `reflection`       | Background “sleep-time” memory consolidation from recent conversations | `auto`            | Read/write |

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
| `description`  | Yes      | When to use this subagent (shown in Task tool and /subagents)                                    |
| `tools`        | No       | Comma-separated list of allowed tools, or `all`. Defaults to `all`.                              |
| `model`        | No       | Model to use (e.g., `haiku`, `sonnet`, `opus`). Defaults to inheriting from main agent.          |
| `memoryBlocks` | No       | Which memory blocks the subagent can access: specific list, `all`, or `none`. Defaults to `all`. |
| `skills`       | No       | Comma-separated list of skills to auto-load                                                      |

### Model and toolset behavior

For the main interactive agent, switching models with `/model` can automatically switch toolsets when toolset mode is `auto` (see [Models and Toolsets](/configuration/models/index.md)).

For subagents, `model` and `tools` are configured independently:

- `model` selects which model the subagent runs on.
- `tools` defines which tools the subagent is allowed to use.
- Deployment access level (`subagent_type`, currently only `general-purpose` when deploying an existing agent) also constrains tool access.

Changing a subagent’s `model` does not automatically change its configured tools.

### System prompt

The body of the Markdown file (after the frontmatter) becomes the subagent’s system prompt. Write clear instructions for what the subagent should do and how it should format its output.

### Override priority

Custom subagents override built-ins with the same name. Project-level subagents (`.letta/agents/`) override global ones (`~/.letta/agents/`).

### Access levels

When deploying an existing agent (via `agent_id`), `subagent_type` must currently be `general-purpose`. That is the only access level accepted on that path. When creating a fresh subagent from a built-in type, the `subagent_type` selects which built-in is used and inherits that built-in’s configured tools and read/write scope. If `subagent_type` is omitted on the deploy path, it defaults to `general-purpose`.
