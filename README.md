# x-claude-code-plugin

An experiment with the [Claude Code native plugin mechanism](https://code.claude.com/docs/en/plugins) — a beta feature that lets you extend Claude Code with custom skills, agents, hooks, and MCP servers packaged as a shareable, versioned directory.

This plugin adds an `/x:date` skill that displays the current date and time.

## Plugin structure

```
x-claude-code-plugin/
├── .claude-plugin/
│   └── plugin.json       # Plugin manifest (name, version, description, author)
└── skills/
    └── date/
        └── SKILL.md      # Skill definition and instructions
```

Skills are namespaced by the plugin name. A skill folder named `date` inside a plugin named `x` is invoked as `/x:date`.

## Test

Load for a single session without installing:

```bash
claude --plugin-dir /path/to/x-claude-code-plugin
```

Then invoke the skill:

```
/x:date
```

Reload changes without restarting:

```
/reload-plugins
```

## Install

Plugins must be installed via a marketplace to persist across sessions. Two options:

**Local marketplace** — add to a personal marketplace like `~/claude-plugins`, then install from it. See the [marketplace docs](https://code.claude.com/docs/en/plugin-marketplaces) for setup instructions.

**Community (GitHub)** — host a `marketplace.json` catalog in a public GitHub repo. Users install with:

```bash
claude plugin marketplace add your-org/your-marketplace
claude plugin install x@your-marketplace
```

## Publish

Submit to the official Anthropic marketplace for broader distribution:

- Claude.ai: [claude.ai/settings/plugins/submit](https://claude.ai/settings/plugins/submit)
- Console: [platform.claude.com/plugins/submit](https://platform.claude.com/plugins/submit)
