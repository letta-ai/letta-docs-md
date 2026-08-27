---
title: Creating agents | Letta Docs
description: Create agents with memory, configure skills and dreaming, and understand agent and conversation IDs
---

Create a stateful agent with `client.createAgent()`. It returns the agent’s ID as a string, which you use to open sessions and manage the agent later.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  persona:
    "You are Quinn, a digital research analyst who can inspect files, run commands, synthesize sources, and maintain living memory about the user's organization.",
  human:
    "The user prefers concise memos with evidence, caveats, and recommended next actions.",
});
// → "agent-3f97f111-3244-41a3-958f-63285dcb412d"
```

## Agents, conversations, and sessions

An **agent** is the persistent entity with memory. A **conversation** is a thread on that agent (`createAgent()` also creates a default one). A **session** is the active connection you use to send messages and stream events. See [Sessions, turns, and durability](/agent-sdk/sessions/index.md) for the full model, ID conventions, and what persists across connections.

## Memory

Set an agent’s starting memory at creation with `persona`/`human` shorthand or explicit `memory` entries:

```
const agentId = await client.createAgent({
  persona: "You are Quinn, a digital research analyst.",
  human: "The user prefers concise memos with evidence and next actions.",
});
```

See [Memory](/agent-sdk/memory/index.md) for how memory is stored, what stays in context, and dreaming.

## Skills

[Skills](/configuration/skills/index.md) are packaged instructions the agent can load for particular kinds of tasks. A skill is a directory containing a `SKILL.md` with frontmatter (`name`, `description`), optionally alongside `scripts/`, `references/`, and `templates/`.

### Skill sources

Control which sources a session exposes with `skillSources`, at agent creation or per session:

```
type SkillSource = "bundled" | "global" | "agent" | "project";


const agentId = await client.createAgent({
  skillSources: ["bundled", "agent"],
});


// Or per session; pass [] to disable skills entirely
await using session = client.createSession(agentId, {
  skillSources: [],
});
```

Each source loads from a specific place on the machine running the harness:

| Source    | Location                                              | Lifetime and scope                                        |
| --------- | ----------------------------------------------------- | --------------------------------------------------------- |
| `bundled` | Shipped with the harness package                      | Read-only; excluded skills vary by backend                |
| `global`  | `~/.letta/skills/`                                    | All agents on that machine                                |
| `agent`   | The agent’s MemFS under `skills/`                     | Travels with the agent; versioned; syncs for cloud agents |
| `project` | `<cwd>/.agents/skills/` (and legacy `<cwd>/.skills/`) | Anything working in that directory                        |

When the same skill ID appears in multiple sources, the more specific one wins: `project` > `agent` > `global` > `bundled`.

“The machine running the harness” depends on the backend. With `backend: "local"`, that’s your machine. With `backend: "cloud"`, global and project directories live on the executing computer — the managed sandbox or your connected computer — not on the SDK host.

### Give an agent its own skills

Agent-owned skills live in the agent’s MemFS under `skills/<name>/SKILL.md`, so they are versioned with the agent’s memory and follow it across machines. Install one from GitHub, a registry, or a URL with the Letta CLI:

```
# GitHub repo, tree URL, SKILL.md URL, or owner/repo/path shorthand
letta skills install anthropics/skills/pdf --agent agent-abc123


# ClawHub registry
letta skills install clawhub/nano-banana-pro --agent agent-abc123
```

The install is committed to the agent’s MemFS git repository and, for cloud agents, synced back to Letta. Agents can also install skills for themselves (the bundled `acquiring-skills` skill teaches them how), or simply write `skills/<name>/SKILL.md` into their memory directly. New skills are discovered on the next message.

### Use skills from `npx skills` or your repository

Vercel’s [`npx skills add`](https://github.com/vercel-labs/skills) installs skills into the cross-tool `.agents/skills/` project directory — which is exactly what Letta’s `project` source reads, so those skills work in sessions whose `cwd` is that project with no extra configuration:

```
npx skills add vercel-labs/agent-skills
```

The same applies to skills you commit to a repository yourself: put them under `.agents/skills/<name>/SKILL.md` and any session working in that checkout picks them up. Letta does not read other tools’ agent-specific directories (`.claude/skills/`, `~/.config/agents/skills/` — where `npx skills add -g` installs), so use the universal `.agents/skills/` project directory, or copy to `~/.letta/skills/` for machine-wide skills.

## Other creation options

```
const agentId = await client.createAgent({
  name: "quinn-research",
  description: "Research analyst for the growth team",
  tags: ["research", "growth"],
  hidden: true, // worker/subagent semantics: hidden from default listings
  baseTools: ["web_search"], // server-side tools; defaults to web_search and fetch_webpage, [] for none
  cwd: "/workspace/project",
});
```

### System prompts

Keep the default system prompt for most agents. It teaches the agent how to use the harness, including tools and memory. Customize `persona`, `human`, and [MemFS](/concepts/memfs/index.md) instead.

Set `systemPrompt` only when your application needs a deliberately different operating model — for example, a narrow pipeline worker that should not behave like a stateful assistant at all:

```
const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  systemPrompt:
    'You are a support-ticket triage classifier. For every message, respond with only a JSON object of the form {"category": string, "severity": "low" | "medium" | "high"}. Do not use tools. Do not add prose.',
});
```

If you find yourself writing a `systemPrompt` that describes who the agent is or how it should communicate, that belongs in the agent’s `persona` memory instead.

`createAgent()` currently accepts custom system prompt strings, not preset names. `systemPrompt` and `disallowedTools` can only be set at agent creation; passing them to `createSession()` or `resumeSession()` throws.

## Manage existing agents

Use `client.agents` to work with agents outside a session:

```
const agents = await client.agents.list();
const agent = await client.agents.retrieve(agentId);
// → { id: "agent-3f97f111-…", name: "agent-d41dd2a0", created_at: "2026-08-11T07:01:45.195Z", … }
await client.agents.update(agentId, { description: "Updated description" });
await client.agents.delete(agentId);
```

Next: [send messages and process the response stream](/agent-sdk/messages/index.md).
