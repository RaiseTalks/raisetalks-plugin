# RaiseTalks plugin

Connect your AI assistant to [RaiseTalks](https://raisetalks.com).

- **Founders** read and update their data room: company, team, market, financials, roadmap, partners and backers.
- **Investors** browse the startup catalog, open data rooms they have access to, and manage their deal pipeline.

This repository is a thin client. It contains the plugin manifests, usage rules and a pointer to the hosted
RaiseTalks MCP server at `https://mcp.raisetalks.com/mcp`. No server code runs on your machine.
You sign in with your existing RaiseTalks account (email and password, Google, or LinkedIn) the first time a tool is used.

## Install

### Cursor

Install **RaiseTalks** from the Cursor Marketplace, or click the install link:

[Add RaiseTalks to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=raisetalks&config=eyJ1cmwiOiJodHRwczovL21jcC5yYWlzZXRhbGtzLmNvbS9tY3AifQ==)

Or add it by hand to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "raisetalks": { "url": "https://mcp.raisetalks.com/mcp" }
  }
}
```

### Claude Code

```
/plugin marketplace add RaiseTalks/raisetalks-plugin
/plugin install raisetalks@raisetalks
```

Or connect only the server, without the skill:

```
claude mcp add --transport http raisetalks https://mcp.raisetalks.com/mcp
```

### ChatGPT and Codex

Search for **RaiseTalks** in the ChatGPT / Codex plugin directory and connect it.

To install from this repository in the Codex CLI:

```
codex plugin marketplace add RaiseTalks/raisetalks-plugin
```

Then open `/plugins` in Codex and install **RaiseTalks**.

### Claude.ai and Claude Desktop

Go to **Settings → Connectors → Add custom connector** and enter `https://mcp.raisetalks.com/mcp`.

## What's included

| Path | Purpose |
| --- | --- |
| `.cursor-plugin/plugin.json` | Cursor plugin manifest |
| `.codex-plugin/plugin.json`, `.agents/plugins/marketplace.json` | ChatGPT / Codex plugin manifest (server address inline) and marketplace entry |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json` | Claude Code plugin manifest and marketplace entry |
| `mcp.json` / `.mcp.json` | Hosted server address (Cursor / Claude Code formats) |
| `dist/raisetalks-openai-plugin.zip` | Upload package for platform.openai.com/plugins (portable Agent Plugins layout). Rebuild with `python3 scripts/build-openai-package.py` after changing `.codex-plugin/plugin.json`, `skills/` or `assets/` |
| `rules/raisetalks.mdc` | Cursor rule with the tools' guardrails |
| `skills/raisetalks/SKILL.md` | How to use the tools well (Cursor, Codex and Claude Code) |

## Notes

- Which tools you see depends on your account: founder accounts get data-room tools, investor accounts get catalog and pipeline tools.
- Editing a data room requires a paid RaiseTalks plan. Reading does not.
- Pitch decks and documents can't be uploaded through the connector. The assistant gives you a link to upload them in the RaiseTalks web app.

## Support

cto@raisetalks.ai

## License

MIT. The license covers this repository's files only. The RaiseTalks service and MCP server are proprietary.
