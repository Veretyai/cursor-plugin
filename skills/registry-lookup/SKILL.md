---
name: registry-lookup
description: >-
  Use when the user needs the raw registry record for a company —
  registration number, legal name, status, address, officers, capital —
  without a full investigation. Uses search_entities then get_entity. The
  covered countries are listed in the server's instructions and at
  verety.ai/developers/mcp; global sources (LEI, ownership, sanctions, ICIJ)
  apply everywhere.
---

# Registry lookup

1. `search_entities` with `name` + `country`, or `registrationNumber` +
   `country` when the user has the official number.
2. Confirm the candidate with the user if more than one is plausible.
3. `get_entity` with the candidate's `id`, or with `country` +
   `registrationNumber` directly.
4. Present the record as the registry holds it: identifiers, legal name,
   status, incorporation date, address, officers, capital. Say which
   registry it came from.

Notes:

- Search and record lookups do not spend a monthly check.
- The record shape differs per registry (`detail` is registry-native). Do
  not normalise fields the registry does not provide.
- If `search_entities` returns `note: "country_not_supported"`, tell the user
  that country is not covered yet and list `supportedCountries` from the
  response. Do not retry with other spellings.
- Some directory-style sources return a listing, not a legal record; if
  `get_entity` reports `unknown_id`, say the source has no detail record and
  offer `investigate` instead.
