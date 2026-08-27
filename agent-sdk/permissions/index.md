---
title: Permissions | Letta Docs
description: Control tool use with permission modes and interactive approvals
---

The SDK gives your application two levers over what an agent’s tools can do: a session-wide **permission mode**, and a **`canUseTool` callback** that approves, denies, or edits individual tool calls — interactively, if your application involves a human.

## Permission modes

Set `permissionMode` at agent creation or per session:

| Mode           | Behavior                                                                                               |
| -------------- | ------------------------------------------------------------------------------------------------------ |
| `standard`     | Default. Tool calls that need approval flow through `canUseTool`                                       |
| `acceptEdits`  | File edits are auto-approved; other approvals still flow through `canUseTool`                          |
| `unrestricted` | Auto-allows tool calls that do not require user input; input-requesting tools still reach `canUseTool` |
| `strict`       | The most restrictive mode; nothing is auto-approved                                                    |

```
await using session = client.createSession(agentId, {
  permissionMode: "standard",
});
```

`allowedTools` is a separate, coarser lever: an availability filter that controls which tools the session exposes at all. See [MCP and client tools](/agent-sdk/mcp/index.md) for how it interacts with client and MCP tools.

## Approve, deny, or edit tool calls

Use `canUseTool` to decide each tool call that isn’t auto-approved. The callback can be fully interactive: return a promise that resolves after your UI or server receives a user’s decision. The SDK keeps the approval pending until the callback returns.

```
await using session = client.createSession(agentId, {
  permissionMode: "standard",
  canUseTool: async (toolName, toolInput) => {
    if (toolName === "Bash") {
      return {
        behavior: "deny",
        message: "Denied by the example approval policy",
      };
    }
    return { behavior: "allow" };
  },
});
```

An `"allow"` response can pass `updatedInput` to edit the tool call before it runs. A `"deny"` response can pass `interrupt: true` to also stop the turn:

```
canUseTool: async (toolName, toolInput) => {
  if (toolName === "Bash") {
    return {
      behavior: "allow",
      updatedInput: { ...toolInput, timeout: 30_000 },
    };
  }
  return { behavior: "deny", message: "Not allowed", interrupt: true };
},
```

The optional third argument gives `canUseTool` details about the approval request. Every field is optional:

| Field                   | Use                                                         |
| ----------------------- | ----------------------------------------------------------- |
| `requestId`             | Correlate logs for the approval request                     |
| `toolCallId`            | Match the approval to a streamed tool call                  |
| `permissionSuggestions` | Show the permissions that the user can grant                |
| `blockedPath`           | Show the path that triggered the permission check           |
| `diffs`                 | Preview proposed file changes before the user approves them |

If the user selects permission suggestions, return their IDs through `updatedPermissions`:

```
return {
  behavior: "allow",
  updatedPermissions: selectedSuggestionIds,
};
```

Tools that ask the user for input also flow through `canUseTool` (even under `unrestricted`), so your app can render the prompt and return the user’s response. Interactive user-input tools like `AskUserQuestion` are always excluded from SDK sessions regardless of `allowedTools`.

## Recover pending approvals

If a client disconnects during approval, the request can remain pending on the active runtime. Resume the conversation and check for pending requests:

```
await using session = client.resumeSession(conversationId, { canUseTool });


const status = await session.getDeviceStatus();
if (status.pendingControlRequests.length > 0) {
  const recovery = await session.recoverPendingApprovals();


  if (recovery.unsupported) {
    throw new Error("This runtime does not support approval recovery");
  }
  if (!recovery.recovered) {
    throw new Error(recovery.detail ?? "Approval recovery failed");
  }
}
```

`pendingControlRequests` in the result from `getDeviceStatus()` lists the approvals waiting on the runtime. If the list is not empty, `recoverPendingApprovals()` sends each request to the `canUseTool` callback for the new session. Keep the approval prompt open until the callback returns. A `recovered: true` response means that the runtime received the recovery command. The user decision can still be pending.

## What to read next

- [Sending messages](/agent-sdk/messages/index.md) — the stream where tool calls and results appear
- [MCP and client tools](/agent-sdk/mcp/index.md) — defining the tools these permissions govern
- [SDK reference](/agent-sdk/reference/index.md) — `CanUseToolCallback` and session option types
