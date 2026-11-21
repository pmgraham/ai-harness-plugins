# AI Harness Plugins

A plugin-first monorepo of cross-harness AI agent plugins (Antigravity, with room for Claude Code, Cursor, and other compatible harnesses).

## Structure

```text
ai-harness-plugins/
├── plugins/
│   └── tiller/
│       ├── .antigravity-plugin/
│       │   └── plugin.json        # Antigravity manifest
│       ├── mcp_config.json        # Antigravity MCP server config
│       ├── rules/AGENTS.md        # Always-on rules
│       ├── skills/<skill>/SKILL.md
│       ├── assets/logo.png
│       └── README.md
└── .github/workflows/validate.yml
```

Each folder under `plugins/<name>/` is a self-contained plugin root. Shared components (`skills/`, `rules/`, `assets/`, `README.md`) live once at `<plugin-root>`, while harness-specific manifests live in their respective dot-directories (e.g., `.antigravity-plugin/plugin.json`, `.claude-plugin/plugin.json`, `.cursor-plugin/plugin.json`).

## Plugins

| Plugin | Description | Harnesses |
| :-- | :-- | :-- |
| [`tiller`](./plugins/tiller) | Personal finance workflows and MCP connection for Tiller Money (`https://ai-tools.tillermoney.com/mcp`) | Antigravity |

## Local Validation & Installation (Antigravity)

```bash
# Validate a plugin (strict)
agy plugin validate --strict ./plugins/tiller

# Install locally into ~/.gemini/config/plugins/
agy plugin install ./plugins/tiller

# Verify installed components
agy plugin list --json
```

## Multi-Tool Validation Note

When adding manifests for other harnesses (e.g., `.claude-plugin/plugin.json`, `.mcp.json`), Antigravity safely ignores those files during packaging. Use the JSON filter in `.github/workflows/validate.yml` (documented in [Antigravity Build Plugins](https://antigravity.google/docs/build-plugins#warnings-in-multi-tool-repositories)) to fail CI on real errors/warnings while ignoring expected other-tool files.
