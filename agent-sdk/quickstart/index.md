---
title: Letta Agent SDK quickstart | Letta Docs
description: Learn the basics of the SDK
---

## Quickstart

Use the Agent SDK to build stateful agents for applications, from personal assistants to digital employees. Create an agent, start a session, and stream its response with JavaScript or TypeScript.

Python applications must use the [App Server WebSocket protocol](/platform/app-server/protocol-lifecycle/index.md) directly.

- [Managed cloud](#tab-panel-0)
- [Local](#tab-panel-1)
- [Remote server](#tab-panel-2)

1. **Get an API key**

   Create an API key from [platform.letta.com/api-keys](https://platform.letta.com/api-keys) and set it as an environment variable:

   ```
   export LETTA_API_KEY='your-api-key-here'
   ```

2. **Install the SDK**

   ```
   npm install @letta-ai/letta-agent-sdk tsx
   ```

3. **Create your code**

   Save this as `quickstart.ts`:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   async function main() {
     const client = new LettaAgentClient({
       backend: "cloud",
       apiKey: process.env.LETTA_API_KEY,
     });


     const agentId = await client.createAgent({
       model: "anthropic/claude-opus-4-8",
       persona:
         "You are Nora, a proactive digital chief of staff. You research, write crisp briefs, remember preferences, and turn ambiguous requests into concrete next steps.",
       human:
         "The user wants concise executive summaries, explicit risks, and suggested follow-up actions.",
     });


     await using session = client.createSession(agentId);


     console.log("Agent ID:", agentId);


     await session.send(
       "Research the launch plan for a small SDK release. Draft a status brief, list the top risks, and propose the first three follow-up tasks.",
     );


     let printedConversationId = false;
     for await (const message of session.stream()) {
       if (!printedConversationId && session.conversationId) {
         console.log("Conversation ID:", session.conversationId);
         printedConversationId = true;
       }
       if (message.type === "assistant") {
         process.stdout.write(message.content);
       }
     }
   }


   main().catch((error) => {
     console.error(error);
     throw error;
   });
   ```

4. **Run your code**

   ```
   npx tsx quickstart.ts
   ```

5. **Example output**

   ```
   Agent ID: agent-abc123
   Conversation ID: conv-abc123
   ## SDK release brief
   - Current state: ...
   - Risks: ...
   - Follow-ups: ...
   ```

Use [shared memory repositories](/agent-sdk/repositories/index.md) to give Cloud agents versioned files. Attach a repository for one session or keep it attached to the agent.

1. **Install Node.js**

   The SDK runs Letta Code locally as a subprocess. Install [Node.js](https://nodejs.org/en/download) version 22.19+.

2. **Install the SDK**

   ```
   npm install @letta-ai/letta-agent-sdk tsx
   ```

3. **Create your code**

   Save this as `quickstart.ts`:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   async function main() {
     const client = new LettaAgentClient({ backend: "local" });


     const agentId = await client.createAgent({
       persona:
         "You are Patch, a resident engineering teammate for this repository. You inspect files before changing them, learn local conventions, and keep a memory of durable codebase patterns.",
       human:
         "The user prefers practical handoffs: architecture notes, commands to run, and gotchas worth remembering.",
     });


     await using session = client.createSession(agentId, {
       cwd: process.cwd(),
     });


     console.log("Agent ID:", agentId);


     await session.send(
       "Inspect this repository and write an onboarding memo for a new engineer: architecture, important workflows, and gotchas.",
     );


     let printedConversationId = false;
     for await (const message of session.stream()) {
       if (!printedConversationId && session.conversationId) {
         console.log("Conversation ID:", session.conversationId);
         printedConversationId = true;
       }
       if (message.type === "assistant") {
         process.stdout.write(message.content);
       }
     }
   }


   main().catch((error) => {
     console.error(error);
     throw error;
   });
   ```

4. **Run your code**

   ```
   npx tsx quickstart.ts
   ```

5. **Example output**

   ```
   Agent ID: agent-abc123
   Conversation ID: conv-abc123
   ## Engineering onboarding memo
   - Architecture: ...
   - Workflows: ...
   - Gotchas: ...
   ```

1) **Start an App Server**

   To keep agent state and the execution environment on the App Server machine, start it with the local backend:

   ```
   letta server --backend local --listen ws://127.0.0.1:4500
   ```

   App Server can also use the cloud backend when you want the execution environment on this machine while agent state remains hosted in Letta Cloud. See [App Server](/platform/app-server/index.md) for deployment and authentication options.

2) **Install the SDK**

   ```
   npm install @letta-ai/letta-agent-sdk tsx
   ```

3) **Create your code**

   Save this as `quickstart.ts`:

   ```
   import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


   async function main() {
     const client = new LettaAgentClient({
       backend: "remote",
       url: process.env.LETTA_APP_SERVER_URL ?? "http://127.0.0.1:4500",
       authToken: process.env.LETTA_APP_SERVER_TOKEN,
     });


     const agentId = await client.createAgent({
       persona:
         "You are Ops, a digital employee running in a shared workspace. You use shell and file tools to inspect systems, prepare handoff reports, and coordinate follow-up work.",
       human:
         "The user values morning briefs with evidence, blockers, owners, and suggested next actions.",
     });


     await using session = client.createSession(agentId, {
       cwd: "/workspace/project",
     });


     console.log("Agent ID:", agentId);


     await session.send(
       "Prepare a morning handoff report: inspect the workspace, summarize recent changes, identify blockers, and list the first actions you recommend.",
     );


     let printedConversationId = false;
     for await (const message of session.stream()) {
       if (!printedConversationId && session.conversationId) {
         console.log("Conversation ID:", session.conversationId);
         printedConversationId = true;
       }
       if (message.type === "assistant") {
         process.stdout.write(message.content);
       }
     }
   }


   main().catch((error) => {
     console.error(error);
     throw error;
   });
   ```

4) **Run your code**

   ```
   LETTA_APP_SERVER_URL='http://127.0.0.1:4500' npx tsx quickstart.ts
   ```

5) **Example output**

   ```
   Agent ID: agent-abc123
   Conversation ID: conv-abc123
   ## Morning handoff
   - Recent changes: ...
   - Blockers: ...
   - Recommended actions: ...
   ```

## Next steps

- [Deployment](/agent-sdk/deployment/index.md) — the cloud, local, and remote backends and where agent state lives
- [Creating agents](/agent-sdk/agents/index.md) — memory, skills, and dreaming
- [Sending messages](/agent-sdk/messages/index.md) — processing reasoning, assistant messages, tool calls, and results
- [Shared memory](/agent-sdk/repositories/index.md) — versioned repositories shared between Cloud agents
- [MCP and client tools](/agent-sdk/mcp/index.md) — expose MCP servers and application functions to sessions
- [Browser and React Native](/agent-sdk/browser/index.md) — the portable client entry point
- [SDK reference](/agent-sdk/reference/index.md) — client methods, session interface, and option types
