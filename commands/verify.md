---
description: Verify a company end to end — search official registries, confirm the candidate, run the investigation, and summarise the report with next steps.
---

# /verify

Verify the company the user names (and country, if given) with Verety.

1. Search with `search_entities`. Use `name` + `country` when both are
   known, otherwise `q` with the user's phrase.
2. List the candidates (name, registry, location, id). Confirm the one to
   use; if exactly one strong match, state it and continue.
3. Run `investigate` on the confirmed `entityId`, passing any website,
   email, address or note the user provided as context.
4. Report: summary; risk and compliance scores with confidence; findings by
   section with their levels and sources; what was not checked; the
   investigator's follow-ups as a short checklist.

Follow the `verify-company` skill and the `verety-accuracy` rule.
