---
title: Troubleshooting | Letta Docs
description: Diagnose common Letta app and CLI setup, connection, and execution problems
---

## Run the built-in diagnostic

Start with `/doctor` when memory structure or context usage looks unhealthy:

```
> /doctor
```

Use `/status` and `/context` to inspect the current agent, model, conversation, and context usage.

## I cannot find an agent on another computer

Confirm that you signed in with the same Letta account on both computers. Agents created without an account are stored only on the machine where they were created and are not backed up to the cloud.

See [Local setup](/self-hosting/index.md) for local storage paths and backup guidance.

## A computer is unavailable in the web app

The desktop app or `letta server` process must remain running on that computer. Check its network connection, then restart the process if the environment does not reconnect.

See [Bring your own machine](/platform/computers/byom/index.md) for setup and connection details.

## A command is waiting for approval

The Letta app and CLI ask before tools perform actions that are not covered by an allow rule. Review the pending action in the interface, or update your permission settings when the action should be allowed consistently.

See [Permissions](/configuration/permissions/index.md).

## A model or provider is missing

Run `/connect` to add or refresh a provider, then use `/model` to choose one of its models.

```
> /connect
> /model
```

For local providers, confirm that Ollama, LM Studio, or llama.cpp is running before reconnecting. See [Local models](/configuration/models#local-models/index.md) for local and cloud-hosted setup options.

## Local state or inference is not where I expected

Local setup controls where agent state is stored; it does not make model inference local by itself. Prompts still go to the selected provider unless you connect a local inference provider.

See [Local setup](/self-hosting#my-prompts-are-still-going-to-a-remote-provider/index.md).

## Collect Desktop logs

Use the Desktop debug panel when you report a Desktop problem:

1. Press `Ctrl+J` on Windows or Linux. Press `Command+J` on macOS.
2. Select **Logs**.
3. Keep the panel open and reproduce the problem.
4. Select **Download**.

Attach the generated `letta-debug-logs-<timestamp>.log` file to the bug report. Review the file before you share it because it can contain sensitive local paths, command output, and error details.

## Get help

If the problem persists, open an issue in the [Letta Code repository](https://github.com/letta-ai/letta-code/issues) or ask in the [Letta Discord](https://discord.gg/letta). Include the Letta Code version, operating system, interface, and the exact error message.
