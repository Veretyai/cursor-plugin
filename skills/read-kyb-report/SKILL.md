---
name: read-kyb-report
description: >-
  Use when the user has a Verety report and asks what it means, whether to
  onboard, or what to do next: how to read riskScore vs complianceScore, what
  LOW/MED/HIGH and PASS/REVIEW/FAIL mean, which findings need a human
  decision, and how to turn followUps into a checklist.
---

# Reading a Verety report

## The two scores

- `riskScore` (0–100, higher = riskier) aggregates the `risk` level of every
  finding: LOW, MED, HIGH.
- `complianceScore` (0–100, higher = cleaner) aggregates the `compliance`
  level: PASS, REVIEW, FAIL.
- Both are computed deterministically from the findings — the same findings
  always give the same scores. They are auditable: "the score is 70 because
  of these findings", never a model's opinion.
- `confidence` (high / medium / low) is about coverage and corroboration,
  not about what was found. Low confidence with a clean score means "we
  could not see much", not "this company is fine".

## What needs a human

- Any finding with `compliance: FAIL` — a hard stop until resolved.
- `compliance: REVIEW` findings — someone must look and decide.
- `risk: HIGH` findings — explain the exposure in one sentence each.
- `unverified[]` — claims the user supplied that could not be confirmed.
- `notChecked[]` — sources that were not consulted and why (not configured,
  unavailable, out of budget). Treat these as open, not as clean.

## Recommending a decision

Never answer "safe to onboard" from the scores alone. Say what the FAIL and
REVIEW items are, what `followUps[]` the investigator wrote, and which of
them close the open points. The decision is the user's.
