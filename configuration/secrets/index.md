---
title: Secrets | Letta Docs
description: Securely store API keys and tokens for your agent to use in shell commands
---

Secrets let your agent use sensitive values like API keys and tokens in shell commands without ever seeing the actual values. The agent writes `$SECRET_NAME` in commands, Letta Code injects the value at execution time, and scrubs it from all output before the agent sees the result.

## Managing secrets

Use the `/secret` slash command to manage your agent’s secrets:

```
> /secret set OPENAI_API_KEY sk-proj-abc123...
Secret '$OPENAI_API_KEY' set.
```

```
> /secret list
Available secrets (2):
  $OPENAI_API_KEY
  $GITHUB_TOKEN
```

```
> /secret unset GITHUB_TOKEN
Secret '$GITHUB_TOKEN' unset.
```

These slash commands are for you. Letta Code shows the agent available secret names automatically in a system reminder at session start and after secret changes.

### Naming rules

Secret names must be uppercase letters, numbers, and underscores only, starting with a letter or underscore. Names are automatically normalized to uppercase.

| Valid          | Invalid                                  |
| -------------- | ---------------------------------------- |
| `API_KEY`      | `api-key` (hyphens not allowed)          |
| `MY_TOKEN_123` | `123_TOKEN` (cannot start with a number) |
| `_PRIVATE`     | `my secret` (no spaces)                  |

## Using secrets in commands

Reference secrets with `$SECRET_NAME` syntax in any shell command:

```
> Can you call the OpenAI API to list my models?


Agent runs: curl -H "Authorization: Bearer $OPENAI_API_KEY" https://api.openai.com/v1/models
```

The agent writes the command with `$OPENAI_API_KEY`. Letta Code injects the actual key value when executing the command, then scrubs the value from the output. The agent never sees `sk-proj-abc123...` in any tool result.

Letta Code scans the shell tool’s command arguments, not the contents of a script. If a script reads a secret from its environment, reference the secret in the launcher command:

Terminal window

```
env GITHUB_TOKEN=$GITHUB_TOKEN ./script.sh
```

### Which tools support secrets?

Secret injection applies to shell execution tools such as `Bash` and `ShellCommand`. `TaskOutput` scrubs output from background shell commands but does not launch commands itself.

Read-only tools like `Read`, `Grep`, and `Glob` do not inject secrets since they don’t execute shell commands.

## How it works

Secrets are protected through multiple layers:

### Substitution at execution time

When the agent calls a shell tool, Letta Code scans the command arguments for `$SECRET_NAME` patterns and injects the referenced secrets as environment variables. The shell expands them during execution. The agent’s tool call in the conversation history always shows the `$SECRET_NAME` placeholder, never the real value.

### Output scrubbing

After a shell command runs, Letta Code scans all output (stdout, stderr, and the full tool response) for any occurrence of a secret value and replaces it with `NAME=<REDACTED>`. This prevents accidental leaks even if a command echoes the value. The placeholder means the secret was injected successfully; it does not mean the value is missing.

### Agent context

Letta Code shows your agent the available secret *names* in a system reminder. Secret values are never added to the agent’s context.

```
The following secrets are set on your agent and available for use:


- `$OPENAI_API_KEY`
- `$GITHUB_TOKEN`
```

### Secret storage

Cloud-agent secrets are stored with the agent on the Letta server and are available across devices. Local-agent secrets are stored in your OS credential manager on that machine.

### Input redaction

When you run `/secret set KEY value`, the value is redacted from the command history. Other users reviewing the conversation will see `/secret set KEY ***`.

## See also

- [Slash commands](/platform/cli/slash-commands/index.md) - Full list of built-in commands
- [Permissions](/configuration/permissions/index.md) - Control what tools your agent can use
