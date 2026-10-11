---
description: Quick registry screen without spending a check — official record, status, identifiers and officers for a named company.
---

# /screen

Pull the official registry record for the company the user names, without a
full investigation (no monthly check is spent).

1. `search_entities` with `name` + `country` (or `registrationNumber` +
   `country`).
2. Confirm the candidate if more than one is plausible.
3. `get_entity` with the chosen id.
4. Present the record as the registry holds it — identifiers, legal name,
   status, address, officers, capital — and name the registry.

If the user then wants sanctions, media, ownership or domain checks, offer
`/verify`, which runs the full investigation.
