---
title: Dynamic Workflows | Letta Docs
description: Orchestrate many subagents from a script your agent writes
applies_to:
  backends:
    - cloud
  interfaces:
    - cli
---

Ask your agent to **use a workflow** when a task needs many [subagents](/configuration/subagents/index.md) working to a fixed plan. The agent writes a short JavaScript script, runs it in the background, and brings the script’s result back to your conversation. You describe the task; the agent writes the script.

Ask for a workflow when one check must cover many files, or when findings should be challenged by independent agents before you see them. For a single focused delegation, ask for a subagent instead.

## Example prompts

- **Audit many files for one issue, with adversarial verification**

  ```
  > Use a workflow to check every file under src/api/ for unvalidated request bodies. Have two independent agents try to refute each finding, and drop the ones they refute.
  ```

- **Review a PR file by file, merged into one ranked list**

  ```
  > Use a workflow to review each file changed in this PR for correctness bugs, then deduplicate the findings and give me one list ranked by severity.
  ```

- **Keep fixing until a check passes**

  ```
  > Use a workflow to run the type check, fix the errors it reports, and repeat until it passes or two rounds make no progress. The fixing agents need edit and shell tools.
  ```

  Subagents get read-only tools (`Read`, `Grep`, `Glob`) by default, so say when a stage must write files or run commands.

- **Research across sources, then cross-check the claims**

  ```
  > Use a workflow to answer this from our docs, the changelog, and the implementation in parallel, then have separate agents verify each claim against those files before summarizing.
  ```

- **Hunt in rounds until nothing new turns up**

  ```
  > Use a workflow to look for race conditions in src/sync/ from several different angles, verify anything new, and stop after two rounds find nothing new.
  ```

- **Draft plans from independent angles and pick one**

  ```
  > Use a workflow to draft three independent migration plans — one optimizing for safety, one for speed, one for reviewability — score them with separate judges, and recommend one.
  ```

Each subagent starts with only the prompt the script gives it: no memory, no conversation history, no skills. Tell your agent what context the stages need.

## Models and cost

One run can spawn dozens of subagent sessions, each with its own context window. Try a new workflow on one directory with a handful of agents before turning it loose on a repository.

By default, subagents run the same model as your agent. However, your agent can also call specific models and mix and match models within the same workflow. Ask your agent to help you optimize cost by using cheaper models for easier tasks (e.g. classifying a large number of files) and stronger models for more challenging verification or writing tasks.

```
> Use a workflow to find dead exports across the repo. Run the search stage on a cheap model at low effort and only the final verification on my current model at high effort. Keep it under 10 agents, and try src/api/ first.
```

Your agent can discover models with `letta model list`, so you do *not* need to manually specify models.

### Limits

Your agent can change the concurrency and each subagent’s timeout and tool-call budget. The other limits are fixed:

| Limit                     | Value                                                                  |
| ------------------------- | ---------------------------------------------------------------------- |
| Subagents running at once | 16 by default; the rest queue                                          |
| Subagents per run         | 1,000                                                                  |
| Per subagent              | 10 minutes, 1,000 tool calls, stopped after 3 identical calls in a row |
| Items per fan-out stage   | 4,096                                                                  |

## Workflow scripts

Scripts are small. A generated one looks like this:

```
export const meta = {
  name: "audit-routes",
  description: "Check each route handler for missing auth",
};


const findings = await pipeline(args.files, (file) =>
  agent(`Check ${file} for missing auth checks. Reply with JSON or null.`, {
    label: file,
    json: true,
  }),
);
return findings.filter(Boolean);
```

`meta` names the run in the status rows, `args` carries the file list the agent collected before launching, each `agent()` call is one subagent, and the returned value is what comes back to your conversation. For the full script API, ask your agent to load its built-in `workflow-authoring` [skill](/configuration/skills/index.md).

## Where subagents run and what they share

Subagents spawned by the workflow run on the same computer, in the same working directory, as your agent. Each subagent’s transcript is kept as its own short-lived conversation linked to your agent. Since it has no memory of its own, it writes nothing back to your agent; the only thing it hands over is its final reply.

Subagents cannot see each other or each other’s conversations. Results move between stages through the script alone: what one stage returns becomes part of the next stage’s prompt. There is no shared scratchpad and no way for two subagents to message each other.
