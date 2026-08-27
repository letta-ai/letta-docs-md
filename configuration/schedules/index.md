---
title: Schedules | Letta Docs
description: Schedule one-time or recurring prompts for Letta agents
---

Scheduled tasks allow you to automate prompts to your agent on a recurring schedule or at a specific time in the future.

Your agent can also schedule tasks itself. Simply ask it in chat.

## Where tasks run

When you schedule a task (`letta cron add`), Letta runs the prompt **where you are working by default**:

- **From a connected computer** (laptop, VM, remote server): The schedule is stored in Letta Cloud, but triggers the prompt on your machine so your agent has access to your local files and tools.
- **From a Cloud sandbox**: Runs in the managed [cloud sandbox](/platform/computers/cloud-sandboxes/index.md).
- **From an unconnected computer**: Creates a local schedule that runs only while your session is active.

### Choosing an execution target

You can override where a task runs using CLI flags:

- `--computer <deviceId>`: Target a specific connected computer (find IDs with `letta environments list`). If the machine is offline when the schedule fires, it falls back to the Cloud sandbox.
- `--runner cloud`: Force execution in the managed Cloud sandbox.
- `--runner local`: Store the schedule strictly on your local machine. It only fires while a Letta session is running and never falls back to the cloud.

Terminal window

```
# Target a specific connected server
letta cron add \
  --agent agent-123 \
  --name "server-check" \
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
  --prompt "Remind me to check staging metrics before deploying." \
  --at "in 45m" \
  --conversation self
```

## Cloud vs. local schedules

|                       | Cloud schedules (Default)                                  | Local schedules (`--runner local`)                     |
| :-------------------- | :--------------------------------------------------------- | :----------------------------------------------------- |
| **Where it’s stored** | Letta Cloud                                                | Local machine (`~/.letta/cron.json`)                   |
| **When it fires**     | Always (server-side timer)                                 | Only while a Letta app, CLI, or server process is open |
| **Timezone**          | Recurring `--cron` runs in **UTC**                         | Evaluated in your **local machine timezone**           |
| **Offline behavior**  | Runs on targeted machine; falls back to sandbox if offline | Pauses until you restart Letta                         |

Local-backend agents always use local schedules; passing `--runner cloud` or `--computer` returns an error. If creating a cloud schedule fails, Letta never silently falls back to local storage.

## Common CLI commands

Terminal window

```
# Add a recurring task (weekdays at 9am UTC)
letta cron add --name "daily-brief" --cron "0 9 * * 1-5" --prompt "Prepare morning briefing."


# Add a one-time reminder
letta cron add --name "standup" --at "10:00am" --prompt "Summarize yesterday's commits."


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

  - Run `letta cron list --agent <id>` and check the task’s `runner` field. A `local` task only fires while a Letta session is connected on the computer that owns it.
  - For a `cloud` task, check its run history with `letta cron runs --id <id>`.

- **My one-time local task disappeared without running**

  - If the listener was down for long enough, the task may have been marked as missed (tasks overdue by >5 minutes).

- **My recurring cloud schedule fires at the wrong time**

  - Recurring `--cron` expressions on cloud schedules are currently evaluated in UTC, not your local timezone.

- **`--computer` says my machine is not connected**

  - The computer must appear in `letta environments list` as a connected machine. Run `letta server` on it (or enable remote access in the Letta app) to connect it to your Letta account.
