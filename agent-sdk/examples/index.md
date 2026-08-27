---
title: Examples | Letta Docs
description: Complete example applications built on the Letta Agent SDK
---

The [SDK repository](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples) ships complete, runnable example applications. Each one demonstrates a different part of the SDK surface:

| Example                                                                                               | What it demonstrates                                                                                                        |
| ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| [web-chat](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/web-chat)                   | A web UI for chatting with an agent — streaming to the browser                                                              |
| [custom-tools](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/custom-tools)           | [Client tools](/agent-sdk/mcp/index.md) that execute locally in the SDK process while the agent runs in a cloud sandbox     |
| [bug-fixer](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/bug-fixer)                 | A stateful agent that finds and fixes bugs, remembering the codebase and past fixes across sessions                         |
| [release-notes](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/release-notes)         | Generating release notes from git commits while learning your formatting preferences over time                              |
| [file-organizer](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/file-organizer)       | A stateful agent that organizes directories and remembers your organizational preferences                                   |
| [research-team](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/research-team)         | A multi-agent research system — persistent memory and collaborative agents that improve over time                           |
| [focus-group](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/focus-group)             | Simulating a political focus group with persistent AI personas to test messaging                                            |
| [economics-seminar](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/economics-seminar) | A multi-agent academic seminar simulation                                                                                   |
| [dungeon-master](https://github.com/letta-ai/letta-agent-sdk/tree/main/examples/dungeon-master)       | A stateful DM that creates its own game system and runs campaigns — persona and [MemFS](/concepts/memfs/index.md) in action |

Clone the repository and run any example from its directory:

```
git clone https://github.com/letta-ai/letta-agent-sdk
cd letta-agent-sdk/examples/web-chat
npm install
```

Each example directory contains its own entry point and, where needed, a README with setup instructions.

## What to read next

- [Quickstart](/agent-sdk/quickstart/index.md) — create your first agent from scratch
- [Creating agents](/agent-sdk/agents/index.md) — memory, skills, and agent configuration
- [MCP and client tools](/agent-sdk/mcp/index.md) — the pattern the custom-tools example uses
- [Shared memory](/agent-sdk/repositories/index.md) — the coordination substrate for multi-agent examples
