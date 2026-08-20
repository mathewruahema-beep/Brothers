---
name: recon-watch
description: Payment and data reconciliation sweep — cross-check Stripe charges, WooCommerce orders, Salesforce Opportunities/Payments and NetSuite postings for a date range, surface mismatches, unreconciled income, refund traceability gaps and sync failures, and turn each exception into tracked work. Use when the user says "reconciliation", "recon check", "unreconciled income", "do the payments match", or "finance says the numbers are off".
---

# Reconciliation Watch

The money path is WooCommerce/Raisely → Stripe → Salesforce → NetSuite, and every hop can drop or duplicate a record. This skill walks the chain so mismatches are found by AI in minutes, not by finance at month-end.

## Prerequisites

Load `birdlife-stripe`, `birdlife-wordpress`, `birdlife-salesforce`, and `birdlife-netsuite` — they carry the known gaps (refund traceability, the unreconciled-income backlog, miniOrange sync behaviour) and the account/object models.

## Workflow

1. **Scope**: confirm the date range (default: last 7 days) and whether to include refunds.
2. **Pull each layer** for the range:
   - Stripe: charges, refunds, disputes, payout totals
   - WooCommerce: orders and their payment references
   - Salesforce: Opportunities/Payments (Payments2Us) created in range, plus sync error logs if visible
   - NetSuite: relevant income postings / undeposited funds (SuiteQL)
3. **Match across layers** on transaction reference, amount, and date proximity. Classify every non-match:
   - `missing-downstream` (e.g. Stripe charge with no Salesforce record — likely sync failure)
   - `missing-upstream` (record with no corresponding charge — investigate manually)
   - `amount-mismatch` (fees vs gross is the usual benign cause — check before flagging)
   - `refund-untraced` (refund in Stripe with no downstream reversal — the known traceability gap)
   - `duplicate`
4. **Report**: totals per layer, match rate, then an exception table with classification and a one-line probable cause each. Distinguish "known systemic gap" from "new anomaly" — the second category is what needs urgent attention.
5. **Track**: on approval, create one Asana task per exception cluster (not per row) with the affected references attached, and/or a Zeus case if it needs the helpdesk trail. Save the run's output to `reports/recon/YYYY-MM-DD.md` and commit, so recurring patterns become visible over time.

## Rules

- Read-only against all financial systems. Never create, modify, or refund anything — exceptions become tasks for a human.
- If a layer can't be queried (auth, missing tool), say so explicitly and mark its matches "unverified" rather than silently narrowing the check.
