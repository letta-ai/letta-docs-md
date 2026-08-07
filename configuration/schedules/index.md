---
title: Schedules | Letta Docs
description: Schedule one-time or recurring prompts for Letta agents
---

Scheduled tasks allow you to automate messages to your agent on a pre-determined schedule. For example, you can have your agent prepare a custom briefing for you every morning at 9am, or have your agent triage your unread emails once an hour.

Your agent can schedule tasks itself. This is the best way to use schedules - simply ask your agent to create a schedule by chatting with it!

## Getting started

The easiest way to manually configure schedules is via the [Letta app](/platform/desktop-app/index.md). Navigate to the **Schedules** tab in the sidebar and follow the on-screen instructions to set up a new schedule.

## Where schedules run

A schedule has two parts: a timer that decides *when* to fire, and a [computer](/platform/computers/index.md) where the prompt executes. There are two kinds of schedules:

- **Cloud schedules** (default for cloud agents): the schedule is stored durably in the cloud and fires from the cloud. By default the prompt executes in the agent’s [cloud sandbox](/platform/computers/cloud-sandboxes/index.md), so the schedule keeps running even when your own devices are offline.
- **Local schedules**: the schedule is stored on the computer that created it and only fires while a Letta app or `letta server` session is running there. Local schedules never leave their computer - if it goes offline, they stop firing.

Agents created on a local backend always use local schedules. Cloud schedules require an agent created on the Letta API.

### Running schedules on your own machine

If the scheduled work needs a specific computer - for example, the files or credentials on a home workstation or a [bring-your-own machine](/platform/computers/byom/index.md) like a cloud VM - you can keep the durable cloud timer and choose that computer as the execution target:

Terminal window

```
letta cron add ... --computer <deviceId>
```

The deviceId comes from `letta environments list`, and the computer must be connected to your Letta account (run `letta server` on it, or enable remote access in the Letta app). If the computer is offline when the schedule fires, execution falls back to the agent’s cloud sandbox, so the task still runs.

Use a local schedule (`--runner local`) only when that fallback is unacceptable and the task should run on its own computer or not at all.

## Setting up schedules via the CLI

You can use the `letta cron` subcommand to manually create schedules:

Terminal window

```
letta cron add \
  --agent agent-123 \
  --conversation default \
  --name "daily-review" \
  --description "Summarize recent code changes every morning" \
  --prompt "Review recent changes and summarize any issues." \
  --cron "0 9 * * *"
```

For a cloud agent this creates a cloud schedule. Add `--runner local` to create a local schedule on the current computer instead, or `--computer <deviceId>` to execute on one of your connected computers.

Use `--every 1d` for a once-daily task at midnight. Use `--cron` when you need a fixed time of day like `9:00am`.

List tasks for the agent:

Terminal window

```
letta cron list --agent agent-123
```

For the full command table, required fields, and defaults, see the [CLI reference](/platform/cli/reference#scheduling/index.md).

## Current behavior and limits

Cloud schedules:

- Fire from the cloud regardless of whether your devices are online.
- One-time (`--at`) times are absolute timestamps, interpreted in your local timezone when created.
- Recurring `--cron` expressions are currently evaluated in UTC. The CLI prints a note about this when you create one; timezone support is planned.
- If creating a cloud schedule fails, no schedule is created - the CLI never silently falls back to local storage.

Local schedules:

- Only execute while a Letta app or `letta server` session is connected on that computer.
- One-shot tasks that are more than 5 minutes late are marked as missed.
- Up to 50 active tasks per agent.
- `--at` values and raw cron expressions are interpreted in the computer’s local timezone.
- `--every 1d` fires daily at local midnight. Use `--cron` for a fixed time of day.

Recurring tasks of both kinds remain active until you delete them. All `letta cron` commands print JSON, so they work well in scripts and wrappers.

## Examples

### Daily review

Terminal window

```
letta cron add \
  --agent agent-123 \
  --name "daily-review" \
  --description "Review recent changes every morning" \
  --prompt "Review recent changes and summarize any issues." \
  --cron "0 9 * * 1-5"
```

### One-time reminder

Terminal window

```
letta cron add \
  --agent agent-123 \
  --conversation default \
  --name "deploy-reminder" \
  --description "Remind me to validate staging before deploy" \
  --prompt "Check staging health, review recent failures, and summarize anything blocking deploy." \
  --at "in 45m"
```

### Recurring check on your own machine

Terminal window

```
letta cron add \
  --agent agent-123 \
  --name "log-watch" \
  --description "Check server logs every hour" \
  --prompt "Inspect the latest logs on this machine and flag anything unusual." \
  --every 1h \
  --computer 0f8a3c1e-9d2b-4f6a-8c5e-7b1d2e3f4a5b
```

## Troubleshooting

- **My task never ran**

  - Run `letta cron list --agent <id>` and check the task’s `runner` field. A `local` task only fires while a Letta session is connected on the computer that owns it.
  - For a `cloud` task, check its run history with `letta cron runs --id <id>`.

- **My one-time local task disappeared without running**

  - If the listener was down for long enough, the task may have been marked as missed.

- **My recurring cloud schedule fires at the wrong time**

  - Recurring `--cron` expressions on cloud schedules are currently evaluated in UTC, not your local timezone.

- **`--computer` says my machine is not connected**

  - The computer must appear in `letta environments list` as a connected machine. Run `letta server` on it (or enable remote access in the Letta app) to connect it to your Letta account.
