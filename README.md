# Verety for Cursor

Verify a business without leaving Cursor. The plugin connects Cursor's agent to
Verety's MCP server, which searches official business registries, returns the
registry record, and runs a full KYB investigation with risk and compliance
scores.

## Tools

| Tool | What it does |
|---|---|
| `search_entities` | Find a company by free text, by name + country, or by registration number + country. Returns candidates with ids. |
| `get_entity` | The full registry record for one company. |
| `investigate` | Registry and domain checks, then agent-driven exploration of additional sources. Returns findings, summary, risk and compliance scores. |

The flow is search → you pick the candidate → investigate. The agent never
guesses which company you meant.

## Install

Install the plugin from the Cursor Marketplace. On first use Cursor opens
Verety in your browser: sign in (or create a free account) and approve the
connection. No key to copy.

Prefer a key? Create one at Account → API keys and add the server by hand in
Settings → MCP:

```json
{
  "mcpServers": {
    "verety": {
      "url": "https://app.verety.ai/api/mcp",
      "headers": { "Authorization": "Bearer vk_live_…" }
    }
  }
}
```

## Try it

- "Find Grupo Bimbo in Mexico."
- "Investigate the first one."
- "Show me the registry record."

## Allowance

Each `investigate` call uses one of your plan's monthly checks (the Free plan
includes 5). Search and record lookups are free. When the allowance is used
up the tool returns `quota_exceeded` with an upgrade link.

## Links

- Docs: https://www.verety.ai/developers/mcp
- Privacy: https://verety.ai/privacy
- Support: legal@verety.ai
