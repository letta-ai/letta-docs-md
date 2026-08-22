---
title: Conversations | Letta Docs
description: Work with one agent across independent message threads
---

A **conversation** is a message thread with an agent. One agent can have many conversations, and every conversation uses the same agent identity and long-term memory.

Use separate conversations to keep tasks independent while preserving what the agent has learned about you and your work.

## When to start a new conversation

Choosing when to start a new conversation is up to user preference. There is no correct answer. Many users tend to have a single, very long main thread. Some users tend to organize agent conversations by topic, such as work, email, or personal. All Letta conversations can be of infinite length, and a long thread alone is not a reason to restart.

## Start and resume conversations

When you run `letta` without arguments, the CLI resumes the default conversation with your last-used agent.

Start a new conversation from the CLI:

```
letta --new
```

Or start one during an interactive session:

```
> /new
```

Use `/resume` to browse previous conversations, or pass a conversation ID directly:

```
> /resume
letta --conv conv-abc123
```

## Fork a conversation

Use `/fork` to branch the current conversation, including its in-context history. The new conversation can take a different direction without changing the original thread.

Use `/btw` for a side question. It forks the conversation in the background and returns the answer without interrupting your main task.

## Conversation context and agent memory

A conversation contains the messages needed for its current thread. As it approaches the model’s context limit, compaction happens automatically: Letta summarizes older messages while keeping recent messages in the active context, so the thread can continue without a manual reset.

A compaction summary can omit exact wording or provenance. The message history remains available, and the agent can use conversation search to recover relevant earlier context.

Long-term knowledge belongs to the agent’s [MemFS memory](/concepts/memfs/index.md), not one conversation. Durable lessons saved there remain available across conversations.
