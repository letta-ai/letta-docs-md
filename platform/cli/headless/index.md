---
title: Headless mode | Letta Docs
description: Run Letta Code non-interactively for scripting and automation
---

Headless mode allows you to run Letta Code non-interactively, making it easy to integrate into scripts, CI/CD pipelines, or compose with other UNIX tools.

## Basic usage

Use the `-p` flag to pass a prompt directly:

Run a one-off prompt

```
letta -p "Look around this repo and write a README.md documenting it"
```

You can also pipe input to Letta Code:

Pipe input

```
echo "Explain this error" | letta -p
```

### Ephemeral runs

Use `--ephemeral` to run a one-shot task without creating, resuming, or persisting an agent, memory blocks, or MemFS. This is ideal for CI/CD pipelines, automated scripts, or disposable tasks where you do not need persistent memory:

Run a stateless one-shot task

```
letta -p "Summarize this repository" --ephemeral
```

Pipe into an ephemeral prompt in CI

```
git diff | letta -p "Review these changes for security issues" --ephemeral --output-format json
```

On the Cloud backend, ephemeral runs use your saved login, create an isolated agent-free conversation, and return `"agent_id": null` in JSON output. On the local backend, runs execute in a temporary scratch store without modifying your saved local agents.

Ephemeral runs accept direct one-shot prompts only. The `--ephemeral` flag cannot be combined with:

- Agent creation or selection (`--agent`, `--name`, `--conversation`, `--new-agent`, `--new`, `--import`, `--resume`, `--personality`, or `--base-tools`)
- State options (`--stateless`, `--memfs`, or `--memfs-startup`)
- Remote environment routing (`--environment` or `--env`)
- Bidirectional mode (`--input-format stream-json`)

### Local backend

Headless mode can use [local setup](/self-hosting/index.md) when you want scripts to run against local agent state:

Run headlessly with local state

```
letta --backend local -p "Summarize this repository"
```

Use `LETTA_LOCAL_BACKEND_DIR` to isolate state for a script or test run:

Use an isolated local backend

```
export LETTA_LOCAL_BACKEND_DIR="$(mktemp -d)"
letta --backend local -p "Inspect this project"
```

### Remote environment routing

Headless mode normally runs in the current Letta Code process. Use `--environment` (or `--env`) to route a one-off prompt through another registered environment by name, device ID, or connection ID:

Run on a registered environment

```
letta -p "Run the test suite" --environment work-laptop
```

Use `--environment cloud` to start or reuse the agent’s cloud sandbox. Run `letta environments list` (or `letta envs list`) to find online environments, and `letta environments current` to show this machine’s registered environment.

Environment-routed prompts use the target environment’s local context and cannot be combined with `--input-format stream-json`.

## Output formats

Letta Code supports three output formats in headless mode:

### Text (default)

Returns the agent’s response as plain text:

Terminal window

```
letta -p "What files are in this directory?"
```

### JSON

Returns a structured JSON response with metadata:

Terminal window

```
letta -p "List all TypeScript files" --output-format json
```

Example output

```
{
  "type": "result",
  "result": "Found 15 TypeScript files...",
  "agent_id": "agent-abc123",
  "conversation_id": "conversation-xyz789",
  "usage": {
    "prompt_tokens": 1250,
    "completion_tokens": 89
  }
}
```

### Stream JSON

Returns line-delimited JSON events for real-time streaming. This is useful for preventing timeouts and getting incremental progress:

Terminal window

```
letta -p "Explain this codebase" --output-format stream-json
```

Each line is a JSON event:

Example stream output

```
{"type":"system","subtype":"init","agent_id":"agent-...","conversation_id":"conversation-...","session_id":"agent-...","model":"claude-sonnet-4-6","tools":[...]}
{"type":"message","message_type":"reasoning_message","reasoning":"The user is asking...","otid":"...","seq_id":1}
{"type":"message","message_type":"assistant_message","content":"Here's an overview...","otid":"...","seq_id":5}
{"type":"message","message_type":"stop_reason","stop_reason":"end_turn"}
{"type":"message","message_type":"usage_statistics","prompt_tokens":294,"completion_tokens":97}
{"type":"result","subtype":"success","result":"Here's an overview...","agent_id":"...","conversation_id":"...","session_id":"...","uuid":"..."}
```

Tool execution appears as paired `tool_call_message` and `tool_return_message` events keyed by `tool_call_id`, including tools executed locally by the CLI. Token-level chunks share the same `otid` (output turn ID) and incrementing `seq_id`.

## Bidirectional mode

For programmatic control, use `--input-format stream-json` to enable bidirectional JSON communication over stdin/stdout. This allows external programs to send messages and receive responses in a structured format.

Start bidirectional mode

```
letta -p --input-format stream-json --output-format stream-json
```

### Input message types

Send JSON messages to stdin (one per line):

User message

```
{
  "type": "user",
  "message": { "role": "user", "content": "What files are here?" }
}
```

Initialize control request

```
{
  "type": "control_request",
  "request_id": "init_1",
  "request": { "subtype": "initialize" }
}
```

Interrupt control request

```
{
  "type": "control_request",
  "request_id": "int_1",
  "request": { "subtype": "interrupt" }
}
```

### Output message types

The CLI emits JSON messages to stdout:

Init event (emitted at session start)

```
{"type": "system", "subtype": "init", "agent_id": "agent-xxx", "conversation_id": "conversation-xxx", "session_id": "agent-xxx", "model": "...", "tools": [...]}
```

Control response

```
{"type": "control_response", "response": {"subtype": "success", "request_id": "init_1", "response": {...}}}
```

Permission request (bidirectional mode)

```
{
  "type": "control_request",
  "request_id": "perm-123",
  "request": {
    "subtype": "can_use_tool",
    "tool_name": "Bash",
    "input": { "command": "ls" }
  }
}
```

Streaming messages

```
{
  "type": "message",
  "message_type": "assistant_message",
  "content": "Hello!",
  "session_id": "...",
  "uuid": "..."
}
```

Result (emitted after each turn)

```
{
  "type": "result",
  "subtype": "success",
  "result": "Hello!",
  "session_id": "...",
  "agent_id": "...",
  "conversation_id": "..."
}
```

### Interactive tool behavior

In one-shot headless mode (`-p` without `--input-format stream-json`), there is no control channel for runtime user input. Tools that require direct user responses, such as `AskUserQuestion`, are excluded from the one-shot headless toolset.

In bidirectional mode (`--input-format stream-json`), permission requests are emitted as `control_request` messages with `subtype: "can_use_tool"`. Your host process should answer with a matching `control_response`.

### Multi-turn conversations

The process stays alive until stdin closes, allowing multi-turn conversations:

Multi-turn example

```
(
echo '{"type": "user", "message": {"role": "user", "content": "Remember: secret is BANANA"}}'
sleep 5
echo '{"type": "user", "message": {"role": "user", "content": "What was the secret?"}}'
) | letta -p --input-format stream-json --output-format stream-json
```

### Token-level streaming

Add `--include-partial-messages` to receive token-level streaming events:

Terminal window

```
letta -p --input-format stream-json --output-format stream-json --include-partial-messages
```

This wraps each chunk in a `stream_event`:

```
{
  "type": "stream_event",
  "event": { "message_type": "assistant_message", "content": "Hel" },
  "session_id": "...",
  "uuid": "..."
}
```

## Agent and conversation selection

By default, headless mode uses the last agent from the current directory and its “default” conversation. Your agent retains memory across all runs, and the default conversation preserves message history between sessions.

To create a new conversation for parallel sessions, use `--new`:

Create a new conversation

```
letta -p "..." --new
```

Create a new agent

```
letta -p "..." --new-agent
```

Run without saving an agent

```
letta -p "..." --ephemeral
```

Use a specific agent

```
letta -p "..." --agent <agent-id>
```

Resume a specific conversation

```
letta -p "..." --conversation <conversation-id>
```

The `--resume` flag is only available in interactive mode (it opens the conversation selector UI). In headless mode, run `letta -p` to continue the default conversation for the current project, or use `--conversation <id>` to resume a specific conversation.

The JSON and stream-json output formats include a `conversation_id` field, which you can use to continue the same conversation in subsequent calls:

Get conversation ID from output

```
result=$(letta -p "Start a new task" --output-format json)
conv_id=$(echo $result | jq -r '.conversation_id')


# Continue the same conversation
letta -p "Continue where we left off" --conversation $conv_id --output-format json
```

## Model selection

Specify a model for the headless run:

Terminal window

```
letta -p "..." --model sonnet
letta -p "..." --model auto
letta -p "..." -m gpt-5-codex
letta -p "..." -m haiku
```

Specify an embedding model when creating a new agent:

Terminal window

```
letta -p "..." --new-agent --embedding letta/letta-free
```

See [Models](/configuration/models/index.md) for the full list of supported model IDs.

## Permission control

### Auto-allow all tools

Use `--yolo` to set permission mode to `unrestricted` and bypass approval prompts unless an explicit deny rule or safety guard blocks the tool call:

Terminal window

```
letta -p "Refactor this file" --yolo
```

### Restrict available tools

The `--tools` flag controls which tools are *attached* to the agent (removing them from the context window entirely):

Only load specific tools

```
letta -p "Analyze this codebase" --tools "Read,Glob,Grep"
```

No tools (conversation only)

```
letta -p "What do you think about this approach?" --tools ""
```

This is different from `--allowedTools`/`--disallowedTools` which control permissions but keep tools in context. See [Permissions](/configuration/permissions/index.md) for more details.

### Permission modes

Auto-allow edits only

```
letta -p "Fix the type errors" --permission-mode acceptEdits
```

Ask before tool use

```
letta -p "Review this PR" --permission-mode standard
```

## Advanced options

### Resume by name

Use `-n` or `--name` to resume an agent by name (case-insensitive). Matches pinned agents or recent agents:

Terminal window

```
letta -p "Continue where we left off" --name myproject
```

### System prompt configuration

Customize the agent’s system prompt when creating new agents:

Use a preset

```
letta -p "..." --new-agent --system letta-claude
```

Use a custom prompt

```
letta -p "..." --new-agent --system-custom "You are a Python expert who writes clean code."
```

**Available presets:**

- `default` - Letta-tuned system prompt
- `letta-claude` - Full Letta Code prompt (Claude-optimized)
- `letta-codex` - Full Letta Code prompt (Codex-optimized)
- `letta-gemini` - Full Letta Code prompt (Gemini-optimized)
- `claude` - Basic Claude (no skills/memory instructions)
- `codex` - Basic Codex
- `gemini` - Basic Gemini

### Memory block configuration

Customize which memory blocks the agent uses:

Specify which preset blocks to include

```
letta -p "..." --new-agent --init-blocks "persona,project"
```

Set values for preset blocks

```
letta -p "..." --new-agent --init-blocks "persona,project" \
  --block-value persona="You are a Go expert" \
  --block-value project="CLI tool for Docker"
```

Use completely custom memory blocks (JSON)

```
letta -p "..." --new-agent --memory-blocks '[
  {"label": "context", "value": "API documentation for Acme Corp..."},
  {"label": "rules", "value": "Always use TypeScript"}
]'
```

No optional blocks (only core blocks)

```
letta -p "..." --new-agent --init-blocks ""
```

**Available preset blocks:**

- `persona` - Agent’s personality and behavior
- `human` - Information about the user
- `project` - Current project context

### Toolset override

Force a specific toolset instead of auto-detection based on model:

Terminal window

```
letta -p "..." --toolset codex    # Codex-style tools
letta -p "..." --toolset gemini   # Gemini-style tools
letta -p "..." --toolset default  # Default Letta tools
```

### Base tools configuration

When creating a new agent with `--new-agent`, specify which base tools to attach:

Specify which base tools to attach

```
letta -p "..." --new-agent --base-tools "memory,web_search"
```

### Create from AgentFile

Create an agent from an AgentFile template or the agent registry:

Terminal window

```
letta -p "..." --import ./my-agent.af
letta -p "..." --import @author/agent-name
```

### System prompt configuration

Customize the agent’s system prompt:

Replace system prompt entirely

```
letta -p "..." --system-custom "You are a helpful assistant that only responds in haiku."
```

### Memory block configuration

Configure memory blocks when creating agents:

Set memory blocks via JSON

```
letta -p "..." --new-agent --memory-blocks '{"persona": "You are a code reviewer", "project": "React app"}'
```

Set individual block values

```
letta -p "..." --block-value "persona=You are a security auditor" --block-value "project=Backend API"
```

## Examples

### Automated tasks

Run lint and fix errors

```
letta -p "Run the linter and fix any errors" --yolo
```

### Structured output for scripts

Use JSON output to parse results programmatically:

Terminal window

```
result=$(letta -p "What is the main entry point of this project?" --output-format json)
echo $result | jq '.result'
```

### Read-only analysis

Use `--tools` to restrict the agent to read-only operations:

Terminal window

```
letta -p "Review this codebase for potential security issues" --tools "Read,Glob,Grep"
```

This section shows shell-level automation around `letta -p`. For built-in server-mode scheduling with `letta cron` and `letta server`, see [Scheduling](/configuration/schedules/index.md).

### Shell cron with `letta -p`

Run Letta Code on a schedule using cron:

Daily code review at 9am

```
0 9 * * * cd /path/to/project && letta -p "Review recent changes and summarize any issues" --tools "Read,Glob,Grep" --output-format json >> /var/log/letta-review.log 2>&1
```

Weekly dependency check

```
0 10 * * 1 cd /path/to/project && letta -p "Check for outdated dependencies and security vulnerabilities" --yolo >> /var/log/letta-deps.log 2>&1
```
