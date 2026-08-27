---
title: Terminology | Letta Docs
description: Canonical names for Letta products, runtimes, and agents
---

Letta’s products share a stateful agent runtime, but differ in how you interact with them, where agent state is stored, and where tools execute. This page defines the names used throughout the documentation.

## Letta

**Letta** is an AI research lab based in San Francisco building machines that learn — also known as [stateful agents](https://www.letta.com/blog/stateful-agents/). [letta.com](https://www.letta.com) is the company and research lab homepage.

In these docs, **Letta** is the umbrella name for the company and its ecosystem, including the hosted platform and open-source products and artifacts. A **Letta agent** is a stateful agent built with Letta. Specific products and services use the qualified names below.

## Letta agent harness

The **Letta agent harness** is the runtime that drives an agent, connects LLMs to persisted context, manages turns, and executes tools. The Letta app, Letta CLI, Letta Agent SDK, and Letta App Server provide different ways to interact with or deploy the harness. Unlike other agent harnesses, Letta’s agent harness is designed for *stateful* agents and is purpose-built to enable agents to build and maintain a consistent yet evolving identity over time (see the [Context Constitution](https://www.letta.com/blog/context-constitution/) for more on stateful agents and identity).

The harness is also called **Letta Code** or the **Letta Code harness**. The Letta CLI, also called the Letta Code CLI, is a minimal terminal interface around the harness. The “Code” in the name refers to code execution: instead of requiring developers to add capabilities primarily by writing server-side tools in TypeScript or Python, the harness executes a preset suite of general-purpose tools client-side and uses [skills as the primary extension mechanism](https://www.letta.com/blog/our-next-phase/). For example, agents can run Bash commands directly on a computer. Although it is particularly strong at software engineering—it was the top OSS model-agnostic harness on Terminal-Bench at [release](https://www.letta.com/blog/letta-code/)—Letta Code is a general-purpose harness designed for many kinds of stateful agents.

## Hosted services and interfaces

### Letta Cloud

**Letta Cloud** is Letta’s hosted service and control plane. The terms **cloud-hosted** and **local** (or “self-hosted”) describe where an agent’s persistent state lives. They do not specify where the agent’s harness or tools execute.

A **cloud-hosted agent** is an agent whose identity, memory, messages, and conversations are stored in Letta Cloud. The same agent can run tools on the current computer, a connected remote computer, or a managed cloud sandbox. Cloud-hosted agents allow for easy teleportation of the same stateful agent from device to device (any device that can reach Letta Cloud via the internet).

A **local agent** or “self-hosted” agent is an agent whose state is stored by a local backend managed by the user (not managed by Letta). A local agent does not require a Letta account and does not appear in the web app or [platform.letta.com](https://platform.letta.com). Here, **local** describes the state backend (managed by Letta vs managed by the user) rather than the physical location of the data. For example, a user can deploy a Letta App Server running the local backend on a remote VPC and store their “local” agents on that VPC. Note that *local state* does not imply *local inference* - users can store their agent state locally while still using remote API services for LLM inference.

**Agent state and computers are independent**

A cloud-hosted agent can work on any supported computer (or “execution environment”) without moving its identity or memory out of Letta Cloud. Choosing a computer determines where tools execute, not where the agent’s persistent state is stored.

For example, a cloud-hosted agent can operate in a cloud sandbox in one conversation, and then be “teleported” onto the user’s local device with the desktop app - the same stateful agent (with the same memory and message history), but running in two execution environments. See [Computers](/platform/computers/index.md) for setup guidance.

Manage API keys, models, usage and billing, and organization settings for Letta Cloud through the web console at [platform.letta.com](https://platform.letta.com). [chat.letta.com](https://chat.letta.com) hosts the Letta web app, which provides the same chat interface for interacting with Letta agents as the desktop app. Common settings, such as model-provider connections, are available directly in both apps.

### Letta API

**Letta API** is the stateful agents REST API at `api.letta.com`. It provides direct server-side access to agents hosted in Letta Cloud, and the Letta API client SDKs wrap it for TypeScript and Python.

The [Letta Agent SDK](/agent-sdk/index.md) is a separate interface built around the Letta agent harness. Unlike the direct REST routes, it is harness-aware: sessions run the harness and its tools. When using the cloud backend, it uses the Letta API underneath.

## Former terminology

[]()

### Constellation

Letta Code versions 0.26.0 through 0.28.13 used **Constellation** for cloud-hosted agents and related sign-in and backend UI. The terminology was retired after 0.28.13 ([#3431](https://github.com/letta-ai/letta-code/pull/3431)).

When reading older documentation, release notes, logs, tests, or source code:

- **Constellation** or **Constellation agent** means **cloud-hosted agent**.
- **Constellation login**, **connect to Constellation**, or **requires Constellation login** means **sign in with Letta**.
- The **Constellation** agent tab or backend is now labeled **Cloud** or described as **Letta Cloud**, depending on context.
- **Constellation sandbox** means **cloud sandbox**.

Constellation described where agent state was stored and how it was accessed. It did not specify where the Letta agent harness or its tools executed.
