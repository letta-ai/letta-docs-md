---
title: Configuration | Letta Docs
description: Configure Letta Code settings and preferences
---

Letta Code uses a hierarchical configuration system with global and project-level settings.

## Backend modes and authentication

On first run, Letta Code asks whether you want to proceed locally or sign in.

Passing `--backend local` or `--backend cloud` overrides the saved startup preference for that invocation. Without an explicit backend flag, Letta Code uses the saved default backend preference.

To change the saved default, run `letta backend local` or `letta backend cloud`. To re-open the interactive first-run menu, run `letta setup`. The legacy `api` backend name remains accepted for compatibility.

### Local mode

[Local setup](/self-hosting/index.md) stores agents and their state on your machine. It does not require a Letta login:

Terminal window

```
letta --backend local
```

### Sign in with Letta

Choose **Sign in with Letta** during first-run setup when you want agents backed up to the cloud and available from `chat.letta.com`, the desktop app, remote environments, schedules, or messaging integrations.

You can force the Letta-hosted backend with:

Terminal window

```
letta --backend cloud
```

### API key

For headless scripts and automation, set an API key directly:

Terminal window

```
export LETTA_API_KEY=your-api-key
```

## Personality presets

Personality presets change the agent’s persona and default memory blocks. Use `/personality` in an interactive session to switch the current agent, or pass `--personality` when creating a new agent:

Terminal window

```
letta --new-agent --personality tutorial
```

Available presets:

| Preset                 | Description                                                      |
| ---------------------- | ---------------------------------------------------------------- |
| `letta-code` or `memo` | Default memory-first Letta Code personality                      |
| `tutorial`             | Tutor guide for new users learning Letta and agent delegation    |
| `blank`                | Minimal starter that asks you to provide the personality prompt  |
| `linus`                | Direct, systems-oriented coding personality                      |
| `kawaii`               | Playful Letta-Chan personality with an `auto-chat` model default |
| `claude`               | Vanilla Claude-flavored source personality                       |
| `codex`                | Vanilla Codex-flavored source personality                        |

The `tutorial`, `linus`, and `kawaii` presets also include onboarding memory by default. The `tutorial` preset is paired with the built-in `letta-help` skill, which guides new users through memory, delegation, tools, skills, search, subagents, and schedules one step at a time.

## Configuration files

### Global settings (`~/.letta/settings.json`)

Applies to all projects:

```
{
  "tokenStreaming": true,
  "globalSharedBlockIds": {
    "persona": "block-id-...",
    "human": "block-id-..."
  }
}
```

### Project settings (`.letta/settings.local.json`)

Personal, gitignored - your agent for this project:

```
{
  "lastAgent": "agent-id-..."
}
```

### Shared project settings (`.letta/settings.json`)

Can be committed to share with your team:

```
{
  "permissions": {
    "allow": ["Bash(pnpm lint)", "Bash(pnpm test)"]
  }
}
```

### File search tuning (`~/.letta/.lettasettings`)

Letta Code also creates a user-local `~/.letta/.lettasettings` file for tuning indexed `@` file search behavior:

\~/.letta/.lettasettings

```
MAX_ENTRIES=50000
```

- `MAX_ENTRIES` controls how many files are kept in the in-memory `@` search cache.
- Raise it for very large repositories if you want more files instantly available in autocomplete.
- Lower it on constrained machines to reduce memory usage.
- Restart Letta Code after changing this file.

### File search exclusions (`.letta/.lettaignore`)

Use `.letta/.lettaignore` to exclude files and directories from indexed `@` file search and disk-scan fallback:

```
node_modules
dist
coverage
*.log
src/generated/**
```

- One glob pattern per line
- `#` starts a comment
- Negation patterns like `!foo` are not currently supported
- Letta Code creates this file automatically with common defaults on first run

You can commit `.letta/.lettaignore` if you want your team to share the same search exclusions.

## Settings reference

| Setting                | Type       | Description                                                           |
| ---------------------- | ---------- | --------------------------------------------------------------------- |
| `tokenStreaming`       | `boolean`  | Enable real-time token streaming                                      |
| `showCompactions`      | `boolean`  | Show compaction event messages in the conversation (default: `false`) |
| `enableSleeptime`      | `boolean`  | Enable sleeptime agents for passive memory updates (default: `false`) |
| `lastAgent`            | `string`   | ID of last used agent (for auto-resume)                               |
| `globalSharedBlockIds` | `object`   | IDs of global memory blocks                                           |
| `permissions.allow`    | `string[]` | Patterns to auto-allow                                                |
| `permissions.deny`     | `string[]` | Patterns to always deny                                               |

## Environment variables

| Variable                  | Description                                                                                           |
| ------------------------- | ----------------------------------------------------------------------------------------------------- |
| `LETTA_API_KEY`           | API key for authentication (alternative to OAuth)                                                     |
| `LETTA_BASE_URL`          | Base URL for a self-hosted Letta server                                                               |
| `LETTA_LOCAL_BACKEND_DIR` | Storage directory for [local setup](/self-hosting/index.md), defaults to `~/.letta/lc-local-backend`  |
| `LETTA_BACKFILL`          | Load message history on agent resume. Set to `0` or `false` to start with clean chat. Default: `true` |
| `LETTA_ENABLE_LSP`        | Enable LSP diagnostics for type error detection. Set to `1` to enable                                 |
| `LETTA_PACKAGE_MANAGER`   | Override detected package manager for auto-updates (`npm`, `bun`, or `pnpm`)                          |
| `DISABLE_AUTOUPDATER`     | Disable automatic updates. Set to `1` to disable                                                      |

## LSP Diagnostics

LSP integration is experimental. Behavior may change in future releases.

Letta Code can integrate with Language Server Protocol (LSP) servers to provide automatic type error detection when reading files.

### Enable LSP

Terminal window

```
export LETTA_ENABLE_LSP=1
```

### Supported languages

| Language              | Extensions                                   | LSP Server                   |
| --------------------- | -------------------------------------------- | ---------------------------- |
| TypeScript/JavaScript | `.ts`, `.tsx`, `.js`, `.jsx`, `.mjs`, `.cjs` | `typescript-language-server` |
| Python                | `.py`, `.pyi`                                | `pyright`                    |

### How it works

When LSP is enabled and you read a supported file:

1. Letta Code starts the appropriate LSP server (auto-installed if missing)
2. The file is analyzed for type errors, syntax errors, and other diagnostics
3. Any errors are appended to the file content in a `<file_diagnostics>` block

```
This file has errors, please fix
<file_diagnostics>
ERROR [10:5] Cannot find name 'foo'
ERROR [15:3] Type 'string' is not assignable to type 'number'
</file_diagnostics>
```

### Behavior

- **Auto-included** for files under 500 lines

- **Manual control** via `include_types` parameter on the Read tool:

  - `include_types: true` - Force include diagnostics (even for large files)
  - `include_types: false` - Skip diagnostics (even for small files)

This helps the agent catch type errors before making edits, reducing iteration cycles.

## Updates

Letta Code automatically keeps itself up to date to ensure you have the latest features and fixes.

- **Update checks**: Performed on startup and periodically while running
- **Update process**: Downloads and installs automatically in the background
- **Applying updates**: Updates take effect the next time you start Letta Code

### Disable auto-updates

Terminal window

```
export DISABLE_AUTOUPDATER=1
```

### Manual update

Terminal window

```
letta update
```

## Recommended .gitignore

```
# Letta Code personal settings
.letta/settings.local.json
```

Keep `.letta/settings.json` tracked to share project context with your team. You can also track `.letta/.lettaignore` if you want shared file-search exclusions.
