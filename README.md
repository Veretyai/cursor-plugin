# Verety for Cursor

KYB and counterparty due diligence inside Cursor. The plugin connects
Cursor's agent to Verety's MCP server, which searches official business
registries, returns the registry record, and runs a full investigation —
registry, domain, sanctions and ownership checks — into findings with risk and
compliance scores.

## What you get

**MCP tools**

| Tool | What it does |
|---|---|
| `search_entities` | Find a company by free text, by name + country, or by registration number + country. Returns candidates with ids. |
| `get_entity` | The full registry record for one company. |
| `investigate` | Registry and domain checks, then agent-driven exploration of additional sources. Returns findings, summary, risk and compliance scores. |

**Skills** — `verify-company` (the search → pick → investigate flow),
`read-kyb-report` (what the scores and findings mean, what needs a human),
`registry-lookup` (the raw record, by country).

**Rule** — `verety-accuracy`: confirm the entity before investigating, one
investigation per entity, sources only, never declare a counterparty
approved.

## Install

Install from the Cursor Marketplace. On first use Cursor opens Verety in
your browser: sign in (or create a free account) and approve the connection.
No key to copy.

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

- "Verify Grupo Bimbo in Mexico with Verety."
- "Find Petrobras in Brazil and show me the registry record."
- "Investigate the first one, we are onboarding them as a supplier."
- "Turn this report into an onboarding checklist."

## Coverage and allowance

The live list of covered countries is on the docs page:
https://www.verety.ai/developers/mcp#coverage. Global sources (LEI, ownership,
sanctions, ICIJ) apply to every company. A search in a country that is not
covered yet says so instead of returning nothing. Each `investigate` call uses one of your plan's monthly checks
(the Free plan includes 5). Search and record lookups are free. When the
allowance is used up the tool returns `quota_exceeded` with an upgrade link.

## Links

- Docs: https://www.verety.ai/developers/mcp
- Privacy: https://verety.ai/privacy
- Support: legal@verety.ai
