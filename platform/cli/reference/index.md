---
title: CLI reference | Letta Docs
description: Command-line options and flags for Letta Code
---

## Essential commands

You’ll likely want to use the following essential commands when using Letta Code:

| Command            | What it does                                   | Example                                  |
| ------------------ | ---------------------------------------------- | ---------------------------------------- |
| `letta`            | Start interactive mode                         | `letta`                                  |
| `letta -p "query"` | Run a query in headless mode                   | `letta -p "commit the changes and push"` |
| `shift-tab`        | Toggle permission modes                        | Press `Shift+Tab`                        |
| `/init`            | Run deep memory initialization (or re-init)    | `> /init`                                |
| `/doctor`          | Audit and refine memory structure              | `> /doctor`                              |
| `/remember`        | Teach your agent something                     | `> /remember always use pnpm`            |
| `/memory`          | View your agent’s memory                       | `> /memory`                              |
| `/model`           | Switch the LLM model                           | `> /model`                               |
| `/login`           | Sign in with Letta                             | `> /login`                               |
| `/search`          | Search past messages                           | `> /search auth bug`                     |
| `/clear`           | Clear context window (messages buffer)         | `> /clear`                               |
| `/context-limit`   | Set or reset the max context window            | `> /context-limit 200000`                |
| `/new`             | Start a new conversation                       | `> /new`                                 |
| `/pin`             | Pin agent for easy access                      | `> /pin`                                 |
| `/agents`          | Swap between agents                            | `> /agents`                              |
| `/feedback`        | Report issues or give feedback                 | `> /feedback`                            |
| `/title`           | Configure the terminal window title            | `> /title`                               |
| `!`                | Enter bash mode to run a bash command directly | `! git status`                           |
| `exit` or `Ctrl+C` | Exit Letta Code                                | `> exit`                                 |

## Basic usage

Terminal window

```
letta [options] [-p "prompt"]
```

| Flag                                  | Description                                                                                                   |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `letta`                               | Resume the default conversation with last-used agent                                                          |
| `letta --new`                         | Start a new conversation (for concurrent sessions)                                                            |
| `letta --resume`, `-r`                | Open conversation selector to browse and resume past sessions                                                 |
| `letta --conversation <id>`, `--conv` | Resume a specific conversation by ID                                                                          |
| `letta --default`                     | Use agent’s default conversation (requires `--agent` or `--name`)                                             |
| `letta -n "Name" --default`           | Use default conversation of agent by name                                                                     |
| `letta --conv default --agent <id>`   | Same as above (explicit form)                                                                                 |
| `letta --conv <agent-id>`             | Shorthand: use default conversation of specified agent                                                        |
| `letta --new-agent`                   | Force create a new agent                                                                                      |
| `letta --import <path>`               | Create new agent from an [AgentFile](/v1-sdk/concepts/agent-file/index.md) (.af) or registry (`@author/name`) |
| `letta --agent <id>`, `-a`            | Use a specific agent by ID                                                                                    |
| `letta --name <name>`, `-n`           | Resume agent by name (matches pinned or recent agents)                                                        |
| `letta --info`                        | Show project info, skills directory, and pinned agents (without starting session)                             |
| `letta --help`                        | Show help                                                                                                     |
| `letta --version`                     | Show version                                                                                                  |

## Backend selection

Letta Code can store agent state through the Letta API or on your local machine. See [Local setup](/self-hosting/index.md) for the full guide.

| Flag                  | Description                                                                   |
| --------------------- | ----------------------------------------------------------------------------- |
| `--backend cloud`     | Use the Letta-hosted backend for signed-in agents and remote access workflows |
| `--backend local`     | Store agents and their state on your local machine                            |
| `--backend <backend>` | Overrides the saved first-run backend preference for this invocation          |

Use `letta backend` to show the saved default, `letta backend cloud` or `letta backend local` to change it, and `letta setup` to re-run the interactive setup menu. The legacy `api` backend name remains accepted for compatibility.

## Model and configuration

| Flag                           | Description                                                      |
| ------------------------------ | ---------------------------------------------------------------- |
| `--model <model>`, `-m`        | Specify model (e.g., `sonnet`, `auto`, `gpt-5-codex`)            |
| `--embedding <model>`          | Specify embedding model for new agents                           |
| `--system <preset>`            | Use a system prompt preset (e.g., `letta-claude`, `codex`)       |
| `--system-custom <text>`       | Use a custom system prompt string (for new agents)               |
| `--personality <name>`         | Personality preset for `--new-agent`                             |
| `--toolset <name>`             | Force toolset: `default`, `codex`, or `gemini`                   |
| `--skills <path>`              | Custom skills directory                                          |
| `--skill-sources <csv>`        | Skill sources: `all,bundled,global,agent,project`                |
| `--no-skills`                  | Disable all skill sources                                        |
| `--no-bundled-skills`          | Disable bundled skills only                                      |
| `--no-system-info-reminder`    | Disable first-turn environment reminder (device/git/cwd context) |
| `--reflection-trigger <mode>`  | Sleeptime trigger: `off`, `step-count`, `compaction-event`       |
| `--reflection-behavior <mode>` | Deprecated - accepted for compatibility but ignored              |
| `--reflection-step-count <n>`  | Sleeptime step-count interval (positive integer)                 |

The `--model` flag can be inconsistent when resuming sessions. Use the `/model` command instead to change models during an interactive session.

Note: When connecting to an existing agent with `--agent <id>`, the agent’s existing configuration (model, toolset) is preserved. Use `/model` or `/toolset` to change them during the session.

To resume your usual working thread, just run `letta`. For parallel work, use `--new`. To reopen a specific thread, use `--conversation <id>` or `--resume` in interactive mode.

## Headless mode

Run Letta Code non-interactively for automation and CI/CD. See [Headless mode](/platform/cli/headless/index.md) for detailed usage.

| Flag                         | Description                                                      |
| ---------------------------- | ---------------------------------------------------------------- |
| `-p "prompt"`                | Run a one-off prompt (headless mode)                             |
| `--output-format <fmt>`      | Output format: `text`, `json`, or `stream-json`                  |
| `--input-format <fmt>`       | Input format: `stream-json` for bidirectional mode               |
| `--include-partial-messages` | Emit `stream_event` wrappers for each chunk (`stream-json` only) |
| `--yolo`                     | Set permission mode to `unrestricted`                            |
| `--permission-mode <mode>`   | Set permission mode: `unrestricted`, `standard`, `acceptEdits`   |
| `--disable-memory-guard`     | Disable the cross-agent memory guard for this parent process     |
| `--tools "Tool1,Tool2"`      | Limit available tools                                            |
| `--allowedTools "..."`       | Allow specific tool patterns                                     |
| `--disallowedTools "..."`    | Block specific tool patterns                                     |
| `--from-agent <id>`          | Inject agent-to-agent system reminder (headless mode)            |
| `--tags <csv>`               | Comma-separated tags for agent organization (headless mode)      |

## Memory configuration

Configure memory blocks when creating new agents.

| Flag                            | Description                                                    |
| ------------------------------- | -------------------------------------------------------------- |
| `--init-blocks <names>`         | Comma-separated preset block names (e.g., `"persona,project"`) |
| `--base-tools <names>`          | Comma-separated base tools to attach when using `--new-agent`  |
| `--memory-blocks <json>`        | JSON array of custom memory blocks                             |
| `--block-value <label>=<value>` | Set value for a preset block (can be specified multiple times) |
| `--memfs`                       | Enable Memory Filesystem for this agent                        |
| `--no-memfs`                    | Disable Memory Filesystem for this agent                       |

## Maintenance

| Flag                                            | Description                                                                                                               |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `letta update`                                  | Manually check and install updates                                                                                        |
| `letta server [options]`                        | Register this environment as a cloud listener                                                                             |
| `letta remote [options]`                        | Alias for `letta server`                                                                                                  |
| `letta connect <provider> [options]`            | Connect provider auth from CLI (same provider flow as `/connect`)                                                         |
| `letta install <source> [--agent <id>]`         | Install a skill (GitHub, Hermes, ClawHub) into an agent MemFS, or install an npm packaged mod globally (`npm:@scope/pkg`) |
| `letta skills list [--agent <id>]`              | List skills installed on an agent                                                                                         |
| `letta skills delete <skill-name> --agent <id>` | Delete a skill from an agent MemFS                                                                                        |
| `letta mods list [--agent <id>]`                | List active mod files and installed packaged mods                                                                         |
| `letta mods enable <spec>`                      | Enable a disabled packaged mod                                                                                            |
| `letta mods disable <spec>`                     | Disable a packaged mod without removing it                                                                                |
| `letta mods update <npm-spec>`                  | Update an installed packaged mod in place                                                                                 |
| `letta mods remove <spec>`                      | Remove a packaged mod                                                                                                     |
| `letta mods package <file> --name <pkg>`        | Scaffold a mod file into a distributable package                                                                          |

## Scheduling

Use `letta cron` to register one-time or recurring prompts for an agent. For cloud agents, schedules are stored durably in the cloud and execute in the agent’s [cloud sandbox](/platform/computers/cloud-sandboxes/index.md) by default; local schedules are stored on the current computer and fire while a session is connected there. See [Scheduling](/configuration/schedules/index.md) for the full guide.

| Command                                                                                          | Description                                                       |
| ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| `letta cron add --name <name> --description <text> --prompt <text> --every <interval> [options]` | Create a recurring task from an interval like `5m`, `2h`, or `1d` |
| `letta cron add --name <name> --description <text> --prompt <text> --at <time> [options]`        | Create a one-time task for a time like `"3:00pm"` or `"in 45m"`   |
| `letta cron add --name <name> --description <text> --prompt <text> --cron "<expr>" [options]`    | Create a recurring task from a raw 5-field cron expression        |
| `letta cron list [--agent <id>] [--conversation <id>] [--runner local\|cloud]`                   | List tasks, optionally filtered by agent, conversation, or runner |
| `letta cron get <id>`                                                                            | Show task details                                                 |
| `letta cron runs --id <id>`                                                                      | Show run history for a task                                       |
| `letta cron delete <id>`                                                                         | Delete one task                                                   |
| `letta cron delete --all --agent <id>`                                                           | Delete all tasks for an agent                                     |

`--agent` defaults to `LETTA_AGENT_ID` when available. `--conversation` defaults to `LETTA_CONVERSATION_ID` or `default`.

Required fields for `letta cron add`:

- `--name`: short label for the task
- `--description`: longer summary of what the task is for
- `--prompt`: the prompt that will be sent when the task fires
- One schedule selector: `--every`, `--at`, or `--cron`
- `--agent <id>` unless `LETTA_AGENT_ID` is already set in the environment

Optional flags for `letta cron add`:

- `--runner local|cloud`: where the schedule lives and fires. Defaults to `cloud` for cloud agents; local-backend agents always use `local`
- `--computer <deviceId>`: (cloud runner only) execute on one of your connected computers instead of the agent’s cloud sandbox, with sandbox fallback if the computer is offline. Get the deviceId from `letta environments list`

Recurring tasks remain active until explicitly deleted. `--every 1d` fires daily at midnight, so use `--cron` for a fixed time of day. Recurring `--cron` expressions on cloud schedules are currently evaluated in UTC.

## Subcommands (JSON-only)

These commands print JSON and are intended for scripting and automation.

| Command                                                     | Description                                                           |
| ----------------------------------------------------------- | --------------------------------------------------------------------- |
| `letta memory status --agent <id>`                          | Show memory repository status for an agent                            |
| `letta memory diff --agent <id>`                            | Show memory conflicts and metadata-only changes                       |
| `letta memory pull --agent <id>`                            | Pull the latest memory repository state                               |
| `letta memory backup --agent <id>`                          | Back up memory to a timestamped directory                             |
| `letta memory backups --agent <id>`                         | List memory backups                                                   |
| `letta memory restore --agent <id> --from <backup> --force` | Restore memory from a backup (destructive)                            |
| `letta memory export --agent <id> --out <dir>`              | Export an agent’s memory filesystem to a directory                    |
| `letta memory tokens [--agent <id>] [--memory-dir <path>]`  | Estimate token usage for the always-loaded `system/` memory directory |
| `letta agents create [options]`                             | Create a memfs-enabled agent                                          |
| `letta agents list [options]`                               | List/search agents                                                    |
| `letta messages search --query <text> [options]`            | Search messages (optionally across all agents)                        |
| `letta messages list [options]`                             | List messages for an agent                                            |
| `letta shared-memory list [--agent <id>]`                   | List shared memory repositories and their attachment state            |
| `letta shared-memory create --name <name>`                  | Create a shared memory repository                                     |
| `letta shared-memory attach <name-or-id> [--agent <id>]`    | Attach a repository to an agent                                       |
| `letta shared-memory detach <name-or-id> [--agent <id>]`    | Detach a repository from an agent                                     |
| `letta shared-memory sync [--agent <id>]`                   | Clone or pull repositories attached to an agent                       |
| `letta shared-memory history <name-or-id> [options]`        | List repository commits                                               |

See [Memory](/concepts/memfs/index.md) for memory and MemFS details, and [Skills](/configuration/skills/index.md) for how skills use these commands. The legacy `letta memfs` subcommand remains an alias for `letta memory`.

Note: For user → agent headless prompts, use `letta -p`. For agent → agent headless prompts, use `letta -p --from-agent <id>`.

## Environment variables

| Variable                  | Description                                                                                                  |
| ------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `LETTA_API_KEY`           | API key for authentication (get yours at [platform.letta.com/api-keys](https://platform.letta.com/api-keys)) |
| `LETTA_BASE_URL`          | Base URL for self-hosted Letta server (e.g., `http://localhost:8283`)                                        |
| `LETTA_LOCAL_BACKEND_DIR` | Storage directory for local agent state. Defaults to `~/.letta/lc-local-backend`                             |
| `LETTA_DEBUG`             | Set to `1` to enable debug logging                                                                           |
| `LETTA_CODE_TELEM`        | Set to `0` to disable anonymous telemetry                                                                    |
| `LETTA_PACKAGE_MANAGER`   | Override detected package manager for auto-updates (`npm`, `bun`, or `pnpm`)                                 |
| `DISABLE_AUTOUPDATER`     | Set to `1` to disable auto-updates                                                                           |
| `MEMORY_DIR`              | Absolute path to the agent’s memory directory (set automatically in shell tools)                             |
| `AGENT_ID`                | Current agent ID (set automatically in shell tools)                                                          |
| `CONVERSATION_ID`         | Current conversation ID (set automatically in shell tools)                                                   |

Set these in your shell profile (`~/.bashrc`, `~/.zshrc`) or `.env` file:

Terminal window

```
export LETTA_API_KEY="your-key-here"
export LETTA_BASE_URL="http://localhost:8283"
```

## Keyboard shortcuts

These shortcuts work during interactive sessions.

| Shortcut      | Description                                                |
| ------------- | ---------------------------------------------------------- |
| `/`           | Open command autocomplete                                  |
| `@`           | Open file autocomplete                                     |
| `!`           | Enter bash mode (run shell commands directly)              |
| `Tab`         | Autocomplete command or file path                          |
| `Shift+Enter` | Insert newline (multi-line input)                          |
| `↑` / `↓`     | Navigate history or menu items                             |
| `Esc`         | Cancel dialog or clear input (double press)                |
| `Ctrl+C`      | Interrupt operation or exit (double press)                 |
| `Ctrl+V`      | Paste content or image                                     |
| `Ctrl+D`      | Hold or release queued messages while the agent is working |

Bash mode lets you run shell commands directly without involving the agent. Press `!` on an empty input line to enter bash mode (prompt changes to `!`), type your command, and press Enter. Press Backspace on an empty line to exit bash mode.
