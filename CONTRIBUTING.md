# Contributing

Thanks for your interest in Vivid MCP.

This repository holds the public description of the Vivid MCP server: the README, the Claude Code plugin manifests and the MCP Registry entry. The server itself runs at `https://api.prime.vivid.money/mcp` and is not open source.

## Structure

```
vivid-mcp/
├── .claude-plugin/   # Claude Code plugin + marketplace
├── .mcp.json         # MCP server config used by the plugin
├── server.json       # MCP Registry entry
└── assets/           # Logo
```

## Guidelines

- Do not commit secrets, API keys, tokens or credentials.
- Keep the client list and the tool names in line with the live server.

## Pull requests

1. Fork the repo and create a branch.
2. Make your changes.
3. Open a PR with a short description of what you changed and why.

Found a problem with the server itself? Open an issue or contact [support@vivid.money](mailto:support@vivid.money).
