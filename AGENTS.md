
        # Project Tree
        ```
        /
    .agents/
        plugins/
            marketplace.json
    .claude-plugin/
        marketplace.json
        plugin.json
    .codex-plugin/
        plugin.json
    .cursor-plugin/
        plugin.json
    .gitignore
    .idea/
        .gitignore
        workspace.xml
    .mcp.json
    LICENSE
    README.md
    assets/
        logo.png
    mcp.json
    rules/
        raisetalks.mdc
    scripts/
        build-openai-package.py
    skills/
        raisetalks/
            SKILL.md
        ```
        # RaiseTalks Plugin - Project Summary

## Overview
**RaiseTalks Plugin** is a thin client that connects AI assistants (Cursor, Claude, ChatGPT/Codex) to the [RaiseTalks](https://raisetalks.com) platform via a hosted MCP (Model Context Protocol) server at `https://mcp.raisetalks.com/mcp`. No server code runs locally.

**Target users:**
- **Founders** — read/update their startup data room (company info, team, market, financials, roadmap, partners, backers)
- **Investors** — browse startup catalog, access data rooms, manage deal pipelines

## Architecture
This is a **client-only repository** containing plugin manifests and configuration files. All server logic is hosted remotely by RaiseTalks.

**Languages/Tools:** JSON manifests, Markdown documentation, Python (for build script)

### Key Components

| Path | Purpose |
|------|---------|
| `.cursor-plugin/plugin.json` | Cursor plugin manifest |
| `.codex-plugin/plugin.json`, `.agents/plugins/marketplace.json` | ChatGPT/Codex plugin manifest & marketplace entry |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json` | Claude Code plugin manifest & marketplace entry |
| `mcp.json` / `.mcp.json` | Hosted MCP server address |
| `dist/raisetalks-openai-plugin.zip` | Upload package for OpenAI plugin platform |
| `rules/raisetalks.mdc` | Cursor rule with tool guardrails |
| `skills/raisetalks/SKILL.md` | Usage guidelines for AI assistants |

## Build Commands
- **Rebuild OpenAI package:** `python3 scripts/build-openai-package.py` (after changing `.codex-plugin/plugin.json`, `skills/`, or `assets/`)

## Installation
- **Cursor:** Install from marketplace or add `{"mcpServers": {"raisetalks": {"url": "https://mcp.raisetalks.com/mcp"}}}` to `~/.cursor/mcp.json`
- **Claude Code:** `/plugin marketplace add RaiseTalks/raisetalks-plugin` or `claude mcp add --transport http raisetalks https://mcp.raisetalks.com/mcp`
- **Claude.ai/Desktop:** Settings → Connectors → Add custom connector → `https://mcp.raisetalks.com/mcp`
- **ChatGPT/Codex:** Search "RaiseTalks" in plugin directory

## Important Notes
- Authentication uses existing RaiseTalks account (email/password, Google, or LinkedIn) on first tool use
- Available tools are **role-dependent** (founder vs. investor account)
- **Editing requires a paid plan**; reading is free
- File uploads (pitch decks, documents) must be done through the RaiseTalks web app — the plugin provides upload links but cannot upload files directly
- Some update operations **replace entire lists** (e.g., `update_team`, list fields in `update_market_product`) — must merge changes with existing data to avoid data loss
- `add_pipeline_note` **replaces** existing notes — read first and append if needed
- Dropdown fields only accept predefined values; don't invent values
- Never fabricate data — leave fields empty rather than guess

## License
MIT (covers repository files only; the RaiseTalks service and MCP server are proprietary)

## Support
cto@raisetalks.ai
        