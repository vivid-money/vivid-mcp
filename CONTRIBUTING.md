# Contributing

Thanks for your interest in contributing to Vivid MCP.

## Structure

```
vivid-mcp/
├── .claude-plugin/          # Claude Code plugin + marketplace
├── .mcp.json                # MCP server config
├── skills/                  # Skills (OpenClaw + Claude Code + AgentSkills)
├── examples/                # Request/response examples
└── docs/                    # Assets and documentation
```

## Adding a new skill

1. Create a folder under `skills/` with a descriptive name.
2. Add a `SKILL.md` with YAML frontmatter (`name`, `description`, `version`) and instructions.
3. Keep `SKILL.md` concise — under 100 lines.
4. Test locally with `claude --plugin-dir .` before submitting.

## Guidelines

- Keep skills platform-agnostic (compatible with Claude Code, OpenClaw, AgentSkills).
- Do not commit secrets, API keys, or credentials.
- Do not hardcode business logic — delegate to MCP tools.
- Write clear, minimal instructions that an AI agent can follow.

## Pull requests

1. Fork the repo and create a branch.
2. Make your changes.
3. Test locally.
4. Open a PR with a short description of what you changed and why.
