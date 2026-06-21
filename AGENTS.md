# AGENTS.md

Guidance for AI agents (Claude Code and others) working in this repository.

## What This Repo Is

A Claude Code **plugin marketplace** (`team-maro`) — a collection of plugins, each in its own folder under `plugins/`. Currently it ships one plugin (`cc-statusline`), but it's structured to hold many.

## Repository Structure

- `.claude-plugin/marketplace.json` — marketplace registry; one entry per plugin, each with `"source": "./plugins/<name>"`
- `plugins/<name>/` — a self-contained plugin:
  - `.claude-plugin/plugin.json` — that plugin's manifest (name, version, author)
  - plus its components (`.mcp.json`, `skills/`, `commands/`, `hooks/`, …)
- `.github/release-please-config.json` + `.github/release-please-manifest.json` — per-plugin release tracking (one `packages` entry keyed by plugin path)
- `.github/workflows/` — CI + release-please

## Plugins

### cc-statusline (`plugins/cc-statusline/`)

Contributes a single MCP server via `plugins/cc-statusline/.mcp.json`:

```json
{ "mcpServers": { "cc-statusline": { "command": "cc-statusline", "args": ["mcp"] } } }
```

It shells out to the user's installed `cc-statusline` binary (must be on `PATH`) in MCP mode — read-only `context_usage`, `rate_limits`, `session_summary` tools backed by `$XDG_CACHE_HOME/cc-statusline/sessions.json`. No runtime code lives here. A change to `.mcp.json` needs `/reload-plugins` or a restart to take effect.

## Adding a plugin

1. `plugins/<name>/.claude-plugin/plugin.json` + components.
2. Append to `.claude-plugin/marketplace.json` (`source: "./plugins/<name>"`).
3. Add `packages["plugins/<name>"]` to `.github/release-please-config.json` and the path to `.github/release-please-manifest.json`.

## Conventions

- **Commits**: Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`…). No `Co-Authored-By` trailer.
- **Releases**: release-please on `master`; SemVer, per-plugin tags (no `v` prefix), e.g. `cc-statusline-0.1.0`. A plugin's release bumps `version` in its `plugin.json`.
- **Formatting**: 2-space indent, UTF-8, LF, final newline (`.editorconfig`).
