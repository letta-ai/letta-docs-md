---
title: Manage shared memory | Letta Docs
description: Create shared memory repositories and attach them to Cloud agents with the Agent SDK
---

Use the Agent SDK to create shared memory repositories, manage their files, and attach them to Cloud agents. See [Shared memory](/concepts/shared-memory/index.md) for the repository model and agent-side Git workflow.

Shared memory APIs and attachments require a `LettaAgentClient` configured with `backend: "cloud"`.

Choose an attachment based on how long the agent needs the repository:

| Need                       | SDK interface                         | Lifetime                                                 |
| -------------------------- | ------------------------------------- | -------------------------------------------------------- |
| Temporary session input    | Session `resources`                   | The SDK removes links it created when the session closes |
| Persistent agent knowledge | `client.agents.repositories.attach()` | The link remains until explicit detachment               |

Cloud agents can also manage persistent attachments through the bundled `managing-shared-memory` skill.

## Create and attach a repository

Create a repository, add files, and pass its ID in the session’s `resources` option:

Repository names must be unique. A name can contain up to 64 letters, numbers, dots, underscores, or hyphens.

```
import { LettaAgentClient } from "@letta-ai/letta-agent-sdk";


const client = new LettaAgentClient({
  backend: "cloud",
  apiKey: process.env.LETTA_API_KEY,
});


const repository = await client.repositories.create({
  name: "launch-inputs",
});


await client.repositories.files.create(repository.id, {
  path: "brief.md",
  content: "# Launch brief\n\nTarget date: September 15\n",
});


const agentId = await client.createAgent({
  model: "anthropic/claude-opus-4-8",
  persona:
    "You are a product operations partner who turns source material into concise, actionable plans.",
});


await using session = client.createSession(agentId, {
  resources: [
    {
      type: "repository",
      repositoryId: repository.id,
    },
  ],
});


await session.send(
  "Read the launch brief, identify missing decisions, and write an action plan.",
);


for await (const message of session.stream()) {
  if (message.type === "assistant") console.log(message.content);
}
```

## Manage files

File helpers are available under `client.repositories.files`:

| Method                         | Description                                              |
| ------------------------------ | -------------------------------------------------------- |
| `list(repositoryId, params?)`  | List files and directories at the current or a given ref |
| `create(repositoryId, params)` | Create a text file                                       |
| `read(repositoryId, params)`   | Read a text file at the current or a given ref           |
| `update(repositoryId, params)` | Replace content, rename a file, or both                  |
| `delete(repositoryId, params)` | Delete a file                                            |

`files.create()` and `files.update()` accept JavaScript strings up to 10 MiB. `files.create()` rejects a new file when the repository contains 2,000 files. Each request performs one file operation. Successful mutations return the resulting commit SHA.

Use a content hash precondition when an update should fail rather than overwrite a file that changed after you read it:

```
const current = await client.repositories.files.read(repository.id, {
  path: "brief.md",
});


const updated = await client.repositories.files.update(repository.id, {
  path: current.path,
  content: `${current.content}\nOwner: Product Operations\n`,
  precondition: {
    contentSha256: current.contentSha256,
  },
});


console.log(updated.commitSha);
```

To rename a file, pass `newPath` to `update()`:

```
await client.repositories.files.update(repository.id, {
  path: "brief.md",
  newPath: "planning/brief.md",
});
```

## Read version history

Each file mutation creates a commit. Use `client.repositories.versions` to list commits and read a file at a particular commit:

```
const versions = await client.repositories.versions.list(repository.id, {
  path: "planning/brief.md",
  limit: 20,
});


const previous = await client.repositories.versions.get(
  repository.id,
  versions[0].sha,
  { path: "planning/brief.md" },
);


console.log(previous.content);
```

`files.list()` and `files.read()` also accept `ref` when you need a consistent historical snapshot.

## Attach a repository persistently

Use a persistent attachment when the repository must remain available after the SDK session closes:

```
await client.agents.repositories.attach(agentId, repository.id);


const attached = await client.agents.repositories.list(agentId);
console.log(attached);
```

Detach the repository when the agent no longer needs it:

```
await client.agents.repositories.detach(agentId, repository.id);
```

## Delete a repository

Delete a repository when your application no longer needs it:

```
await client.repositories.delete(repository.id);
```

The repository no longer appears in SDK list or retrieval results. The SDK has no restore method.

See the [SDK reference](/agent-sdk/reference#cloud-repository-client/index.md) for all repository methods and types.
