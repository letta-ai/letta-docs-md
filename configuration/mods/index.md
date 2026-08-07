---
title: Mods | Letta Docs
description: Customize Letta Code with trusted local code
---

Mods run as fully trusted code inside your Letta Code process. They let your agent modify its own runtime — adding tools, commands, event hooks, permission policies, and provider adapters that take effect immediately on reload. This makes the harness self-modifying: your agent can extend its own capabilities, shape how turns and tools behave, and adapt the environment around itself over time.

Mods are for changing the harness itself. If you want to teach your agent how to do a task, ask it to write a [skill](/configuration/skills/index.md). If you want to alter the limitations of the harness, ask it to write a mod.

Browse packaged mods in the [Mods catalog](https://www.letta.com/agent/mods/) or inspect their source in the [letta-ai/mods GitHub repository](https://github.com/letta-ai/mods).

## Ask your agent to write mods

Mods are designed to be written and modified by agents. Letta Code agents have access to the deeper mod documentation inside the codebase and can create or update mods far more efficiently than writing them by hand.

For example, ask:

```
Write a Letta Code mod that adds a /review command for reviewing my current git diff.
```

Your agent can inspect any existing files in `~/.letta/mods/`, write the new mod, and tell you to run `/reload` when it is ready.

## Setup

Mods live in your global Letta directory:

```
~/.letta/mods/
```

Each `.js`, `.mjs`, `.ts`, or `.tsx` file in that directory is loaded on startup. After editing a mod, run `/reload` to reload it without restarting Letta Code.

Mods are trusted code. They run locally with the same access as Letta Code, so only install or write mods you trust.

### Desktop support

Mods load in the local Letta Code process used by both terminal and Desktop sessions. Mod commands, tools, event hooks, and permission rules work in both interfaces. Terminal panels and statusline renderers only appear in the terminal UI.

## Example

A mod exports an `activate` function. Inside `activate`, register the capabilities you want and return a cleanup function if the mod owns timers, UI, or subscriptions.

\~/.letta/mods/whereami.ts

```
export default function activate(letta) {
  if (!letta.capabilities.commands) return;


  return letta.commands.register({
    id: "whereami",
    description: "Show the active agent and working directory",
    run(ctx) {
      return {
        type: "output",
        output: `Agent: ${ctx.agent.name ?? ctx.agent.id}\nCWD: ${ctx.cwd}`,
      };
    },
  });
}
```

Now `/whereami` is available in Letta Code.

## What mods can do

Here’s what’s possible:

### Commands

Add custom `/commands` that send a prompt to the agent or run local logic and return output directly. Commands can also work in the background while the main agent is busy, using a forked conversation handle for their own model calls.

### Tools

Register agent-callable tools that the model can invoke autonomously during a session. Mod tools run locally and can access your filesystem, run shell commands, or call local services — anything the process can reach. Tools can be conditionally registered so they only appear in context when relevant, keeping the tool surface lean.

### Events

Subscribe to lifecycle and execution events. Some events are observe-only; others accept a return value that influences what happens next.

| Event                | What you can do                                                                                                        |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `conversation_open`  | Initialize mod state, log context, or branch on how the session started (`startup`, `new`, `resume`, `fork`, `reload`) |
| `conversation_close` | Persist state, log session stats, or trigger cleanup                                                                   |
| `tool_start`         | Modify tool arguments before execution, or return a synthetic result to bypass the tool entirely                       |
| `tool_end`           | Rewrite or redact the tool result before the agent sees it                                                             |
| `turn_start`         | Inject context, rewrite messages, or cancel a user turn before it reaches the model                                    |
| `turn_end`           | Chain another turn automatically by injecting a follow-up message                                                      |
| `llm_start`          | Observe each model request before it’s sent, including the model, message count, and context window                    |
| `llm_end`            | Observe each model response or provider error, including stop reason, token usage, and duration                        |
| `compact_start`      | Checkpoint important state before compaction evicts it                                                                 |
| `compact_end`        | Inspect what changed, log stats, or re-inject persistent context                                                       |

`llm_start`, `llm_end`, `compact_start`, and `compact_end` fire only for local agents, where inference and compaction run on your machine. For agents running through the Letta API, this work happens server-side, so these events don’t fire there.

### Permissions

Add dynamic allow/ask/deny policies that evaluate before a tool call is executed. Useful for enforcing safety rules, auditing specific operations, or requiring confirmation for sensitive actions.

### Providers

Register a custom model/API provider that local agents can use. Provider mods are local-only — they do not add providers for agents running through the Letta API.

### UI

Surface custom UI in the terminal. Mods can show **panels** — live text around the input bar for things like status, progress, the current time, or your active git branch. The bottom **statusline** is one of these slots; set it up with the `/statusline` command (see [Statusline](#statusline) below). Mods can also **ask you a question** — a prompt where you pick from options or type an answer, and the mod waits for your response before continuing. For example, a deploy mod could ask which environment to target before it runs.

### Statusline

Replace the bottom statusline in the TUI with a custom renderer. You can show anything that fits on one line — git branch, active agent, token usage, current working directory, or whatever is useful for your workflow. Ask your agent with `/statusline` or just describe what you want.

## Packaged mods

Beyond single mod files, mods can be distributed as npm packages. Packaged mods include their own dependencies and are installed into a managed registry so they can be enabled, disabled, or updated independently.

Install a packaged mod:

```
letta install npm:@scope/package-name
```

For example, install the optional [Goal Mode mod](https://github.com/letta-ai/mods/tree/main/packages/goal-mode) to add the `/goal` command and goal lifecycle tools:

```
letta install npm:@letta-ai/goal-mode
```

Manage installed packages:

```
letta mods list                        # show mod files and installed packages
letta mods enable <package-spec>
letta mods disable <package-spec>
letta mods update npm:@scope/package   # update to the latest version in place
letta mods remove <package-spec>
```

Your agent can also scaffold a mod file into a distributable package:

```
letta mods package <mod-file> --name <package-name>
```

## Diagnostics and logging

Mods can report diagnostics — structured messages your agent can read and act on. This is useful for surfacing setup errors, missing configuration, or runtime problems that the agent should investigate and fix.

Ask your agent to add diagnostics to a mod:

```
Add diagnostics to my review mod so I can see if it fails to find the git repo on startup.
```

Your agent can add `letta.diagnostics.report()` calls to the mod:

\~/.letta/mods/review\.ts

```
export default function activate(letta) {
  const repoPath = process.env.REPO_PATH;
  if (!repoPath) {
    letta.diagnostics.report({
      message: "REPO_PATH is not set — /review will not work",
      severity: "error",
    });
  }
  // ...
}
```

Diagnostics are written to:

```
~/.letta/mods/diagnostics/latest.json
```

Your agent has access to this file and can read it directly to investigate mod problems. If something is broken, just ask:

```
Check my mod diagnostics and fix whatever is wrong.
```

## Debugging

Errors in individual mods are caught automatically — a broken mod is skipped and its error recorded to diagnostics, so Letta Code still starts normally. To run without any mods at all for a clean baseline, use:

```
letta --no-mods
```

or:

```
LETTA_DISABLE_MODS=1 letta
```
