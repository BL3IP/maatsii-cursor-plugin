# Maatsii — LinReg MCP (Cursor plugin wrapper)

Public wrapper for the **Maatsii** remote MCP server. This repository does **not** contain the MCP server source code. The live server runs at:

**https://mcp.maatsii.com/mcp**

Streamable HTTP · no API key · no auth

## What it does

Maatsii is a vision-first technical analysis MCP for markets:

- **200 live chart frames** across **25 groups** (index futures, rates, FX, crypto, energy, metals, ETFs, mega-cap, volatility, and more)
- Charts redraw about every **3 seconds** with LinReg fan rails (EQ / R / S), multi-timeframe labels, and a printed price box
- **64 active setups** (45 Fan + 19 Tick) plus an **11-section multi-timeframe TA** framework
- Your AI reads annotated JPEG charts directly (not OHLC tables)

Website: [maatsii.com](https://maatsii.com)

## How to configure

### Cursor (recommended)

Add a remote MCP server pointing at the hosted endpoint (no key):

```json
{
  "mcpServers": {
    "maatsii": {
      "url": "https://mcp.maatsii.com/mcp"
    }
  }
}
```

Or install the **Maatsii** plugin from the Cursor Marketplace (this repo’s `mcp.json` / `plugin.json` wire the same URL).

### Claude Code

```bash
claude mcp add --transport http maatsii https://mcp.maatsii.com/mcp
```

### Claude Desktop / other stdio bridges

```json
{
  "mcpServers": {
    "maatsii": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.maatsii.com/mcp"]
    }
  }
}
```

### ChatGPT / VS Code / other MCP clients

Add remote connector URL: `https://mcp.maatsii.com/mcp` · authentication: **none**.

## How to use

1. Confirm the connector exposes **10 tools**.
2. Ask for an analysis, for example: `11-section TA on all NQ charts`.
3. Or fetch one pane: `Get NQ 15M (c4) and read the fan levels off the right axis`.

### Tools

| Tool | Purpose |
| --- | --- |
| `maatsii_get_group` | Fresh charts for a group (inline JPEGs + URLs) |
| `maatsii_get_chart` | One chart by id (`c1`–`c200`) or ticker (`NQ_100T`) |
| `maatsii_chart_map` | 200-chart / 25-group map and aliases |
| `maatsii_reading_guide` | Right axis, last-price tag, fan labels |
| `maatsii_fan_guide` | EQ / R / S rails, confluence, slope |
| `maatsii_analysis_framework` | 11-section MTF TA structure |
| `maatsii_list_setups` | 64 active setups (45 Fan + 19 Tick) |
| `maatsii_get_setup` | Full playbook for one setup id |
| `maatsii_match_setup` | Optional hint matcher from vision features |
| `maatsii_get_concept` | Short methodology explanations |

### Frame URLs (optional, no MCP client required)

```bash
curl -o nq.jpg "https://api.maatsii.com/c1.jpg?raw=1&cb=$(date +%s)"
```

Always use `?raw=1` and a fresh `cb=` cachebuster.

## What’s in this repo

- `mcp.json` — points Cursor at `https://mcp.maatsii.com/mcp`
- `plugin.json` / `.cursor-plugin/` — Cursor plugin manifest
- `skills/` — optional skill instructions for agents
- `assets/logo.svg` — logo
- `LICENSE` — MIT

Server source stays private / hosted. This public repo exists so registries and Copilot can show a clear README and repository URL.

## Official registry

- Name: `com.maatsii/linreg`
- Version: `1.5.2`
- Endpoint: `https://mcp.maatsii.com/mcp`

## License

MIT
