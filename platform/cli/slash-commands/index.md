---
title: Slash commands | Letta Docs
description: Control Letta Code's behavior during an interactive session with slash commands
---

Control Letta Code’s behavior during an interactive session with slash commands. Press `Tab` to autocomplete command names.

## Built-in slash commands

Commands are also available from autocomplete: type `/` in an interactive CLI session and press `Tab`.

### Common session commands

| Command            | Description                                               |
| ------------------ | --------------------------------------------------------- |
| `/agents`          | Browse agents (pinned, Letta Code, all)                   |
| `/model`           | Switch model                                              |
| `/init`            | Initialize or re-initialize your agent’s memory           |
| `/doctor`          | Audit and refine your memory structure                    |
| `/remember [text]` | Ask the agent to remember something from the conversation |
| `/memory`          | View your agent’s memory                                  |
| `/palace`          | Open the Memory Palace in your browser                    |
| `/search [query]`  | Search messages across agents                             |
| `/connect`         | Connect LLM API keys and coding plans                     |
| `/clear`           | Clear in-context messages                                 |
| `/chdir <path>`    | Change the working directory for the current TUI session  |

### Agent and conversation management

| Command                                          | Description                                                     |
| ------------------------------------------------ | --------------------------------------------------------------- |
| `/new`                                           | Start a new conversation with the current agent                 |
| `/resume [id]`                                   | Browse and resume past conversations, or switch directly by ID  |
| `/fork`                                          | Fork the current conversation                                   |
| `/btw <question>`                                | Fork the conversation and ask a side question in the background |
| `/pin [-l]`                                      | Pin the current agent globally, or locally with `-l`            |
| `/unpin [-l]`                                    | Unpin the current agent globally, or locally with `-l`          |
| `/rename agent [name]` or `/rename convo [name]` | Rename the current agent or conversation                        |
| `/description <text>`                            | Update the current agent’s description                          |
| `/export`                                        | Export the current agent as an AgentFile (`.af`)                |

### Memory, tools, and configuration

| Command                                               | Description                                            |
| ----------------------------------------------------- | ------------------------------------------------------ |
| `/reflect [transcript_file]`                          | Launch a reflection agent                              |
| `/sleeptime`                                          | Configure reflection trigger settings                  |
| `/compaction`                                         | Configure compaction mode settings                     |
| `/compact [all\|sliding_window]`                      | Summarize conversation history immediately             |
| `/memfs [enable\|disable\|sync\|reset]`               | Manage filesystem-backed memory                        |
| `/toolset`                                            | Switch toolset (`default`, `codex`, or `gemini`)       |
| `/experiments`                                        | Toggle local experiments                               |
| `/reload`                                             | Reload settings and restart TUI effects                |
| `/system`                                             | Switch system prompt                                   |
| `/personality`                                        | Switch to a personality preset                         |
| `/subagents`                                          | Manage custom subagents                                |
| `/mcp`                                                | Manage MCP servers                                     |
| `/secret <set\|list\|unset> [key] [value]`            | Manage secrets for shell commands                      |
| `/skills`                                             | Browse available skills by source                      |
| `/skill-creator [description]`                        | Enter guided skill creation mode                       |
| `/memory-repository <set\|unset\|status\|push> [url]` | Push the agent memory repo to an additional git remote |

### Interface and maintenance

| Command                                | Description                                               |
| -------------------------------------- | --------------------------------------------------------- |
| `/usage`                               | Show session usage statistics and balance                 |
| `/context`                             | Show context window usage                                 |
| `/context-limit [tokens] [--override]` | Set or reset the max context window                       |
| `/recompile`                           | Recompile the current agent and conversation              |
| `/feedback`                            | Send feedback to the Letta team                           |
| `/hooks`                               | Manage hook configuration                                 |
| `/statusline [request]`                | Customize the CLI footer statusline                       |
| `/title`                               | Configure the terminal window title                       |
| `/reasoning-tab [on\|off\|status]`     | Toggle the `Tab` shortcut for reasoning tiers             |
| `/terminal [--revert]`                 | Set up or remove terminal shortcuts such as `Shift+Enter` |
| `/ade`                                 | Open the current agent in ADE in your browser             |
| `/install-github-app`                  | Set up the Letta Code GitHub Action in this repository    |
| `/login`                               | Sign in with Letta                                        |
| `/disconnect <provider>`               | Disconnect an existing provider account                   |
| `/bg`                                  | Show background shell processes                           |
| `/exit`                                | Exit this session                                         |
| `/logout`                              | Clear credentials and exit                                |

`/skill-creator` replaces the older `/skill` shortcut in the interactive CLI.

## Customizing the statusline

Use `/statusline` to change the bottom row of the CLI. Describe what you want and Letta Code will guide the setup:

Terminal window

```
/statusline show my git branch, current model, and remaining context
```

Custom statuslines are global and live at `~/.letta/extensions/statusline.tsx`. They render while the input row is idle; safety prompts and transient CLI hints can still temporarily replace them. If you edit the file by hand, run `/reload` to reload it.

## Goal mode

`/goal` is provided by the optional [Goal Mode mod](https://github.com/letta-ai/mods/tree/main/packages/goal-mode), rather than as a built-in command. Install the packaged mod from a terminal:

```
letta install npm:@letta-ai/goal-mode
```

Run `/reload` or restart Letta Code after installation. The command is then available in both terminal and Desktop sessions.

Use `/goal` to keep a concrete objective active across turns:

Terminal window

```
/goal improve benchmark coverage
```

The mod stores the goal for the current conversation and adds a reminder at the start of each turn. It tracks active time and observed token usage, provides a soft token budget, and adds tools that let the agent inspect and update the goal. It does not change your permission mode or automatically start another turn.

Write a specific, verifiable objective. For example: “Run all tests, fix every failure, and stop only when the full suite passes” is more useful than “improve the project.”

Common goal commands:

| Command                                  | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| `/goal` or `/goal status`                | Show the current goal and recorded usage |
| `/goal --token-budget 50000 <objective>` | Set a goal with a soft token budget      |
| `/goal --replace <objective>`            | Replace the current goal                 |
| `/goal pause`                            | Pause goal reminders                     |
| `/goal resume`                           | Resume a paused goal                     |
| `/goal complete`                         | Manually mark the goal complete          |
| `/goal clear` or `/goal disable`         | Remove the goal                          |

Before the agent marks a goal complete, the mod prompts it to audit the objective against real evidence such as files, command output, tests, or PR state.

## Invoking skills

Skills are normally loaded by the agent when relevant, but you can invoke a specific skill directly with slash syntax:

Terminal window

```
/<skill-name> [optional instructions]
```

For example:

Terminal window

```
/acquiring-skills find a browser testing skill
```

Use `/skills` to browse available skills by source. Direct skill invocation loads the named skill’s instructions, then continues with the rest of your request. See [Skills](/configuration/skills/index.md) for skill installation, scopes, and authoring.

## Custom slash commands

Custom slash commands let you define frequently used prompts as Markdown files that Letta Code can execute. Commands can be project-specific (shared with your team) or personal (available across all projects).

### Syntax

```
/<command-name> [arguments]
```

| Parameter        | Description                                                       |
| ---------------- | ----------------------------------------------------------------- |
| `<command-name>` | Name derived from the Markdown filename (without `.md` extension) |
| `[arguments]`    | Optional arguments passed to the command                          |

### Command types

#### Project commands

Commands stored in your repository and shared with your team. These show “(project)” in `/help`.

**Location**: `.commands/`

Terminal window

```
# Create a project command
mkdir -p .commands
echo "Review this code for security vulnerabilities:" > .commands/security.md
```

#### Personal commands

Commands available across all your projects. These show “(user)” in `/help`.

**Location**: `~/.letta/commands/`

Terminal window

```
# Create a personal command
mkdir -p ~/.letta/commands
echo "Explain this code in simple terms:" > ~/.letta/commands/explain.md
```

### Arguments

Pass dynamic values to commands using argument placeholders:

**All arguments with `$ARGUMENTS`**

.commands/fix-issue.md

```
Fix issue #$ARGUMENTS following our coding standards
```

Usage: `/fix-issue 123 high-priority` → `$ARGUMENTS` becomes “123 high-priority”

**Positional arguments with `$1`, `$2`, etc.**

.commands/review-pr.md

```
Review PR #$1 with priority $2 and assign to $3
```

Usage: `/review-pr 456 high alice` → `$1`=“456”, `$2`=“high”, `$3`=“alice”

### Dynamic content

Execute shell commands when the slash command runs using `` !`command` `` syntax:

```
Current branch: !`git branch --show-current`
Recent commits:
!`git log --oneline -5`
```

Shell commands are executed and replaced with their output.

### File references

Include file contents using the `@` prefix:

```
Review the implementation in @src/utils/helpers.js


Compare @src/old-version.js with @src/new-version.js
```

### Frontmatter

Command files support frontmatter for metadata:

| Property        | Purpose                                    | Default              |
| --------------- | ------------------------------------------ | -------------------- |
| `description`   | Brief description shown in `/help`         | First line of prompt |
| `argument-hint` | Arguments expected (shown in autocomplete) | None                 |

**Example:**

.commands/review\.md

```
---
description: Review code changes in the current branch
argument-hint: "[focus area]"
---


Review all uncommitted changes in this repository. Focus on:


- Code quality and best practices
- Potential bugs or edge cases
- Suggestions for improvement


$ARGUMENTS
```

### Priority

Project commands (`.commands/`) take precedence over global commands (`~/.letta/commands/`). Custom commands appear in autocomplete alongside built-in commands.

## Skills vs slash commands

**Slash commands** are best for replacing common prompts you send to the agent—quick shortcuts for frequently used instructions.

**Skills** are better for complex, repeatable action prompts because they’re pinned to the context window when loaded and survive compaction. This means the agent always has access to the skill’s instructions, even after long conversations.

[Learn more about Skills →](/configuration/skills/index.md)

### Use slash commands for

**Quick, frequently used prompts:**

- Simple prompt snippets you use often
- Quick reminders or templates
- Frequently used instructions that fit in one file

**Examples:**

- `/review` → “Review this code for bugs and suggest improvements”
- `/explain` → “Explain this code in simple terms”
- `/optimize` → “Analyze this code for performance issues”

### Use Skills for

**Comprehensive capabilities with structure:**

- Complex workflows with multiple steps
- Capabilities requiring scripts or utilities
- Knowledge organized across multiple files
- Team workflows you want to standardize

**Examples:**

- Code review Skill with security checklist, performance patterns, and linting scripts
- Documentation Skill with style guides and templates
- Deployment Skill with environment-specific configs and validation

### Key differences

| Aspect                  | Slash Commands             | Skills                                           |
| ----------------------- | -------------------------- | ------------------------------------------------ |
| **Complexity**          | Simple prompts             | Complex capabilities                             |
| **Structure**           | Single `.md` file          | Directory with `SKILL.md` + resources            |
| **Context**             | Injected once when invoked | Pinned to context when loaded                    |
| **Survives compaction** | No                         | Yes                                              |
| **Discovery**           | Explicit (`/command`)      | Agent loads automatically or via `/<skill-name>` |
| **Scope**               | Project or personal        | Project, agent, global, or bundled               |

### Example comparison

**As a slash command:**

.commands/review\.md

```
Review this code for:


- Security vulnerabilities
- Performance issues
- Code style violations
```

Usage: `/review` (one-time injection)

**As a Skill:**

```
.skills/code-review/
├── SKILL.md (overview and workflows)
├── SECURITY.md (security checklist)
├── PERFORMANCE.md (performance patterns)
└── STYLE.md (style guide reference)
```

Usage: Agent loads the skill automatically, or you invoke it directly with `/code-review`, and it has persistent access to all reference material throughout the conversation.

## See also

- [Skills](/configuration/skills/index.md) - Create comprehensive capabilities with multiple files
- [Memory & dreaming](/configuration/memory/index.md) - Initialize, teach, and improve agent memory
- [CLI reference](/platform/cli/reference/index.md) - Command-line options and flags
