---
title: GitHub action | Letta Docs
description: Integrate Letta Code into your GitHub repository
---

The easiest way to set up the GitHub action is to ask a Letta agent to do it for you: open the [Letta app](/platform/desktop-app/index.md) or CLI in your repository and ask your agent to install the Letta Code GitHub action.

The [Letta Code GitHub action](https://github.com/letta-ai/letta-code-action) lets you trigger Letta agents directly from GitHub issues and pull requests. Mention `@letta-code` in any comment to get help with code questions, implementation, and reviews.

## Quick start

1. Get an API key from [platform.letta.com/api-keys](https://platform.letta.com/api-keys)
2. Add `LETTA_API_KEY` to your repository secrets
3. Create `.github/workflows/letta.yml`:

```
name: Letta Code


on:
  issue_comment:
    types: [created]
  issues:
    types: [opened, assigned]
  pull_request_review_comment:
    types: [created]


jobs:
  letta:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      issues: write
      pull-requests: write
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 1
      - uses: letta-ai/letta-code-action@v0
        with:
          letta_api_key: ${{ secrets.LETTA_API_KEY }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

Now mention `@letta-code` in any issue or PR comment.

## Triggers

The action runs when explicitly triggered:

| Trigger      | How it works                                                              |
| ------------ | ------------------------------------------------------------------------- |
| **Mention**  | Include `@letta-code` in a comment, issue body, or PR body                |
| **Label**    | Add the `letta-code` label to an issue (configurable via `label_trigger`) |
| **Assignee** | Assign a specific user to an issue (configure via `assignee_trigger`)     |
| **Prompt**   | Set the `prompt` input for automated workflows                            |

Replying to a comment without `@letta-code` will *not* trigger the action.

## Conversations

The GitHub Action supports persistent conversations that continue across multiple interactions.

### Issue conversations

Each issue gets its own conversation, labeled as `owner/repo/issue-N`. When you mention `@letta-code` multiple times in the same issue, the agent remembers the full context of previous interactions.

### PR conversations

PRs can either:

- **Start a new conversation** if the PR doesn’t reference an issue
- **Continue an issue’s conversation** if the PR references an issue (via “Fixes #N”, “Closes #N”, etc.)

This means when you create a PR that fixes an issue, the agent already has the full context from the issue discussion.

### Viewing conversations

Each agent response includes a link to view the conversation in the [Letta web app](https://chat.letta.com):

```
🤖 Agent: Memo • View job run
💻 Chat with this agent in your terminal: letta --conv conv-abc123
```

You can continue the conversation locally using the CLI command shown.

## Configuration

| Input                      | Description                                                 | Default       |
| -------------------------- | ----------------------------------------------------------- | ------------- |
| `letta_api_key`            | Your Letta API key                                          | Required      |
| `github_token`             | GitHub token for API access                                 | Required      |
| `agent_id`                 | Specific agent ID to use (auto-discovers if not set)        | None          |
| `prompt`                   | Auto-trigger with this prompt                               | None          |
| `trigger_phrase`           | Phrase that activates the agent                             | `@letta-code` |
| `model`                    | Model to use (`opus`, `sonnet`, `haiku`, `auto`, `gpt-4.1`) | `opus`        |
| `assignee_trigger`         | Username that triggers when assigned                        | None          |
| `label_trigger`            | Label that triggers the action                              | `letta-code`  |
| `path_to_letta_executable` | Path to a custom Letta CLI                                  | None          |
| `allowed_bots`             | Comma-separated bot usernames allowed to trigger (or `*`)   | None          |
| `allowed_non_write_users`  | Users allowed without write permissions                     | None          |

### Using a specific agent

To use the same agent across all issues/PRs in your repository:

```
- uses: letta-ai/letta-code-action@v0
  with:
    letta_api_key: ${{ secrets.LETTA_API_KEY }}
    github_token: ${{ secrets.GITHUB_TOKEN }}
    agent_id: agent-586a9276-1e95-41f8-aaa4-0fb224398a01
```

This is useful when you want the agent to have shared memory across all repository interactions.

### Using the latest CLI

To ensure you’re using the latest Letta CLI:

```
steps:
  - uses: actions/checkout@v4


  - name: Install latest Letta Code
    id: letta-bin
    run: |
      npm install -g @letta-ai/letta-code@latest
      echo "path=$(command -v letta)" >> "$GITHUB_OUTPUT"


  - uses: letta-ai/letta-code-action@v0
    with:
      letta_api_key: ${{ secrets.LETTA_API_KEY }}
      github_token: ${{ secrets.GITHUB_TOKEN }}
      path_to_letta_executable: ${{ steps.letta-bin.outputs.path }}
```

## Bracket syntax

Pass arguments directly from your comment:

```
@letta-code [--model haiku] quick question about this code
@letta-code [--new-agent] start with a fresh agent
@letta-code [--new-agent --model sonnet] new agent with a specific model
```

Multiple flags can be combined in a single bracket.

## Agent persistence

The agent ID is stored in a hidden HTML comment in the tracking comment. On follow-up mentions, the action finds this metadata and resumes the same agent, preserving conversation history and memory.

To force a new agent, use: `@letta-code [--new-agent] start fresh`

## Automated workflows

For workflows that run automatically (e.g., auto-review every PR):

```
on:
  pull_request:
    types: [opened]


jobs:
  auto-review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: letta-ai/letta-code-action@v0
        with:
          letta_api_key: ${{ secrets.LETTA_API_KEY }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
          prompt: "Review this PR for bugs and security issues"
```

## Custom bot identity

To have comments appear as `your-app[bot]` instead of `github-actions[bot]`, use a GitHub App:

```
steps:
  - uses: actions/checkout@v4
  - name: Generate GitHub App token
    id: app-token
    uses: actions/create-github-app-token@v1
    with:
      app-id: ${{ secrets.APP_ID }}
      private-key: ${{ secrets.APP_PRIVATE_KEY }}
  - uses: letta-ai/letta-code-action@v0
    with:
      letta_api_key: ${{ secrets.LETTA_API_KEY }}
      github_token: ${{ steps.app-token.outputs.token }}
```

## Security

By default, only repository collaborators with write access can trigger the action. This prevents unauthorized users on public repos from consuming your API credits.

Use `allowed_bots` for bot users or `allowed_non_write_users` to allow specific usernames without write permissions (use with caution).

## Capabilities

**What it can do:**

- Read and search files in your repository
- Make edits and create new files
- Run shell commands (git, npm, etc.)
- Commit and push changes
- Create pull requests
- Update its tracking comment with progress

**What it can’t do:**

- Approve PRs (security restriction)
- Modify workflow files (GitHub restriction)

## CLI companion

Continue chatting with the same agent locally using [Letta Code](/index.md):

Terminal window

```
# Install
npm install -g @letta-ai/letta-code


# Resume the agent from GitHub
letta --agent agent-xxxxx


# Or resume a specific conversation
letta --conv conv-xxxxx
```

The agent ID and conversation ID are shown in every GitHub comment footer.

## Troubleshooting

**Agent not responding?**

- Check that `LETTA_API_KEY` is set in repository secrets
- Verify the workflow has the required permissions
- Look at the Actions tab for error logs

**Wrong agent resumed?**

- Use `@letta-code [--new-agent]` to force a fresh agent

**Want to see what the agent is doing?**

- Click “View job run” in the comment footer
- Enable `show_full_output: true` in your workflow for detailed logs
