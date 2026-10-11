---
name: verify-company
description: >-
  Use when the user asks to verify, vet, screen, or run KYB/KYC due diligence
  on a company, supplier, customer, or counterparty. Covers the full flow:
  search official registries with search_entities, let the user pick the right
  candidate, then run investigate and present the report — summary, risk and
  compliance scores, findings by section, what was not checked and why. Never
  guesses which company was meant.
---

# Verify a company with Verety

## Flow

1. **Search.** Call `search_entities`. Prefer `name` + `country` (ISO code)
   when both are known; use `registrationNumber` + `country` for an exact
   lookup; use `q` (free text, e.g. "Grupo Bimbo Mexico") when the user gave
   only a phrase.
2. **Let the user pick.** Show the candidates as a short list: name,
   registry, location, id. If there is exactly one strong match, say which
   one you intend to use and proceed; if several are plausible, ask. Do not
   investigate a guess.
3. **Investigate.** Call `investigate` with the chosen `entityId`. Pass what
   the user already knows as context (`website`, `email`, `address`, `note`)
   — it is verified against, not trusted. Set `goals` to match the ask:
   `compliance` (default), `risk`, `partnership`, `employer`, `contractor`.
   Expect 10–40 seconds, longer the first time after idle.
4. **Present.** Lead with `summary`, then `riskScore` / `complianceScore`
   with `confidence`, then findings grouped by `section`, each with its
   `risk` (LOW/MED/HIGH) and `compliance` (PASS/REVIEW/FAIL) and the sources
   it came from. Close with `notChecked[]` (what was skipped and why) and
   `followUps[]` (manual actions the investigator recommends).

## Rules of thumb

- One `investigate` per confirmed entity. It spends one of the account's
  monthly checks; do not re-run to "double check".
- `coverage: "baseline_only"` means the exploration layer did not run —
  say so; the report is registry and domain checks only.
- Findings come only from consulted sources. Do not add claims from your own
  knowledge; if something is missing, it belongs in "not checked".
- If the tool returns `quota_exceeded`, tell the user and give the
  `upgradeUrl`. Do not retry.
