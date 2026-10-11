---
description: Turn a Verety report into a supplier or customer onboarding checklist — open items, documents to request, and who must sign off.
---

# /onboarding-checklist

From the most recent Verety report in this conversation (run `/verify` first
if there is none), produce an onboarding checklist:

1. **Blocking items** — every finding with `compliance: FAIL`, one line each
   with the source.
2. **Needs review** — `compliance: REVIEW` and `risk: HIGH` findings, with
   who should decide (compliance, legal, procurement).
3. **Documents to request** — derived from `unverified[]` and
   `notChecked[]`: what evidence would close each open point (e.g. a
   certificate of good standing, proof of address, beneficial-ownership
   declaration).
4. **Investigator follow-ups** — `followUps[]` as actions, verbatim intent.
5. **Sign-off** — a final line stating the decision is pending the items
   above; never mark the counterparty approved.

Output as a markdown checklist the user can paste into a ticket.
