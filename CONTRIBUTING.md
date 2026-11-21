# Contributing

Contributions are welcome — whether you are adding a new plugin, extending an existing plugin to another AI harness, improving rules/skills, or fixing documentation.

## Repository Layout

Each plugin lives in its own self-contained directory under `plugins/<name>/`:

```text
plugins/<name>/
├── .antigravity-plugin/
│   └── plugin.json        # Antigravity manifest
├── mcp_config.json        # MCP server configuration (optional)
├── rules/AGENTS.md        # Always-on guardrails (optional)
├── skills/<skill>/
│   └── SKILL.md           # Skill instructions (optional)
├── assets/logo.png        # Plugin icon
└── README.md              # Setup and usage documentation
```

Shared components (`skills/`, `rules/`, `assets/`, `README.md`) live once at the plugin root. Harness-specific manifests (such as `.antigravity-plugin/plugin.json`, `.claude-plugin/plugin.json`, or `.cursor-plugin/plugin.json`) live in their respective dot-directories.

## Adding or Updating a Plugin

1. **Manifest**: Ensure `plugin.json` uses a kebab-case `name`, semantic `version`, non-empty `displayName`, `description`, `logo`, `author`, and `license`.
2. **Documentation**: Include a clear `plugins/<name>/README.md` with setup instructions and example prompts, and update the plugins table in the root [README.md](./README.md).
3. **Safety & Privacy**: Never commit secrets, credentials, or personal data. Skills and rules that mutate external state (spreadsheets, APIs, databases) should require explicit user confirmation before writing.
4. **Versioning**: Bump `version` in `plugin.json` when modifying plugin behavior.

## Local Validation

Before opening a pull request, validate your changes locally:

```bash
# Strict Antigravity plugin validation
agy plugin validate --strict ./plugins/<name>

# Verify all JSON files parse cleanly
find plugins -type f -name '*.json' -exec jq empty {} +
```

## Pull Requests

- Keep each PR focused on a single plugin or change.
- Follow [Conventional Commits](https://www.conventionalcommits.org/) (for example, `feat(tiller): ...`, `fix(tiller): ...`, `docs: ...`).
- Complete the PR checklist and make sure CI passes.

## Code of Conduct

Participation in this project is governed by the [Code of Conduct](./CODE_OF_CONDUCT.md).
