---
title: Permissions | Letta Docs
description: Control what tools your agent can use
---

Press `Shift+Tab` in interactive mode to cycle through `unrestricted`, `acceptEdits`, and `standard`.

Letta Code supports [**human-in-the-loop**](/v1-sdk/tools/human-in-the-loop/index.md) approval flows. By default, the interactive CLI starts in `unrestricted` mode. Switch to `standard` when you want Letta Code to ask before running tools that require approval.

## Permission modes

You can adjust how much approval is required:

| Mode                    | Behavior                                                                                     |
| ----------------------- | -------------------------------------------------------------------------------------------- |
| `unrestricted` (`yolo`) | Auto-allow tool calls unless blocked by explicit deny rules or safety guards                 |
| `standard`              | Ask before running tools that require approval, such as shell commands, edits, and subagents |
| `acceptEdits`           | Auto-allow file edits, prompt for other approval-requiring tools                             |
| `strict`                | Ask before every tool call, including reads, skills, and normally safe shell commands        |

### Using permission modes

Ask before tool use

```
letta -p "Review this codebase" --permission-mode standard
```

Require approval for every tool

```
letta -p "Audit this environment" --permission-mode strict
```

Auto-allow edits

```
letta -p "Fix the type errors" --permission-mode acceptEdits
```

Bypass prompts

```
letta -p "Run the full test suite and fix failures" --yolo
```

The `--yolo` flag is shorthand for `--permission-mode unrestricted`. Select `strict` explicitly with `--permission-mode strict`; it is not part of the `Shift+Tab` cycle. Legacy values such as `default` and `bypassPermissions` are still accepted for compatibility and map to `standard` and `unrestricted` respectively.

In `letta server`, permission mode is tracked per conversation and restored after server restarts.

### Cross-agent memory guard

Letta Code protects other agents’ memory directories before normal permission rules run. A tool call that targets another agent’s memory directory is denied even in `unrestricted` mode.

The current agent can access its own memory. Subagents can also access their parent agent’s memory through the parent-agent scope passed by Letta Code. If you intentionally need a parent process to maintain another agent’s memory, start it with `--disable-memory-guard`:

Disable memory guard for this parent process

```
letta --disable-memory-guard
```

This flag is ignored by subagents; their memory guard remains enabled.

## Fine-grained control

### Allow/deny specific patterns

Control permissions for specific tool invocations:

Allow specific commands

```
letta --allowedTools "Bash(npm run lint),Bash(npm run test)"
```

Block dangerous patterns

```
letta --disallowedTools "Bash(rm -rf:*)"
```

### Persistent rules

Set rules in `.letta/settings.json` that apply every session:

.letta/settings.json

```
{
  "permissions": {
    "allow": ["Bash(pnpm lint)", "Bash(pnpm test)", "Read(src/**)"],
    "deny": ["Bash(rm -rf:*)", "Bash(git push --force:*)", "Read(.env)"]
  }
}
```

### Pattern syntax

| Pattern             | Matches                        |
| ------------------- | ------------------------------ |
| `ToolName`          | All uses of a tool             |
| `ToolName(pattern)` | Specific arguments             |
| `**`                | Wildcard for paths             |
| `:*`                | Wildcard for command arguments |

## Restricting available tools

Separately from permissions, you can control which tools are loaded at all using `--tools`:

Only load read-only tools

```
letta -p "Analyze this code" --tools "Read,Glob,Grep"
```

No tools (conversation only)

```
letta -p "Explain this concept" --tools ""
```

This removes tools from the agent’s context entirely, not just permission-gating them.
