---
title: Schedules | Letta Docs
description: Schedule one-time or recurring prompts for Letta agents
applies_to:
  backends:
    - cloud
    - local
  interfaces:
    - web
    - desktop
    - cli
---

Scheduled tasks allow you to automate prompts to your agent on a recurring schedule or at a specific time in the future.

Your agent can also schedule tasks itself. Simply ask it in chat.

## Where tasks run

When you schedule a task (`letta cron add`), Letta Code stores it based on **where you are working**:

- **From a Cloud sandbox**: The schedule is stored in Letta Cloud and runs in the managed [cloud sandbox](/platform/computers/cloud-sandboxes/index.md).
- **From a computer connected with `letta server`**: The schedule is stored in Letta Cloud and runs on that computer.
- **From an interactive CLI or Desktop session, `--backend local`, or a server without schedule support**: Creates a local schedule that runs only while a Letta Code session is active on that computer.

### Choosing an execution target

Cloud schedules accept `--computer <deviceId>` to target a specific connected computer (find IDs with `letta computers list`). If the computer is offline when the schedule fires, that run fails with `TARGET_DEVICE_UNAVAILABLE`; it does not fall back to the Cloud sandbox.

Terminal window

```
# Target a specific connected server
letta cron add \
  --agent agent-123 \
  --name "server-check" \
  --description "Hourly server health check" \
  --prompt "Check system health and report any disk warnings." \
  --every 1h \
  --computer <deviceId>
```

## Choosing the conversation

By default, every scheduled run starts a **new conversation**. This prevents recurring tasks from bloating your agent’s context window or cluttering your primary chat history.

To send runs to an existing conversation instead:

- `--conversation default`: Send every run to the agent’s main conversation.
- `--conversation <id>`: Send runs to a specific conversation thread.
- `--conversation self`: Bind to the conversation you’re currently having with the agent.

Terminal window

```
# Remind you in your current conversation
letta cron add \
  --agent agent-123 \
  --name "deploy-reminder" \
  --description "Staging metrics reminder" \
  --prompt "Remind me to check staging metrics before deploying." \
  --at "in 45m" \
  --conversation self
```

## Cloud vs. local schedules

|                       | Cloud schedules                             | Local schedules                             |
| :-------------------- | :------------------------------------------ | :------------------------------------------ |
| **Where it’s stored** | Letta Cloud                                 | Local machine (`~/.letta/crons.json`)       |
| **When it fires**     | Always (server-side timer)                  | Only while a CLI or Desktop session is open |
| **Offline behavior**  | Run fails if the target computer is offline | Pauses until you restart Letta Code         |

Recurring `--cron` and `--every` expressions are evaluated in **UTC**. Passing `--computer` for a local schedule returns an error. If creating a cloud schedule fails, Letta Code never silently falls back to local storage.

## Common CLI commands

Terminal window

```
# Add a recurring task (weekdays at 9am UTC)
letta cron add --name "daily-brief" --description "Weekday morning briefing" --cron "0 9 * * 1-5" --prompt "Prepare morning briefing."


# Add a one-time reminder
letta cron add --name "standup" --description "Daily standup summary" --at "10:00am" --prompt "Summarize yesterday's commits."


# List scheduled tasks
letta cron list


# View run history for a task
letta cron runs --id <taskId>


# Delete a task
letta cron delete <taskId>
```

For the full command table and options, see the [CLI reference](/platform/cli/reference#scheduling/index.md).

## Troubleshooting

- **My task never ran**

  - Check its run history with `letta cron runs --id <id>`. A local task only fires while a Letta Code session is open on the computer that owns it.
  - A cloud task targeting a computer fails with `TARGET_DEVICE_UNAVAILABLE` if that computer was offline at fire time.

- **My one-time local task disappeared without running**

  - If Letta Code was closed for long enough, the task may have been marked as missed (tasks overdue by >5 minutes).

- **My recurring schedule fires at the wrong time**

  - Recurring `--cron` and `--every` expressions are evaluated in UTC, not your local timezone.

- **`--computer` says my machine is not connected**

  - The computer must appear in `letta computers list` as a connected machine. Run `letta server` on it to connect it to your Letta account. `--computer` only works for cloud schedules.
