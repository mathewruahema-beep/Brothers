---
name: incident-log
description: Structured incident management — capture a live incident's timeline as it unfolds, draft stakeholder comms, coordinate checks across Cloudflare/WordPress/M365/Salesforce/Stripe, and produce the post-incident review with Asana follow-up actions. Use when something is down, degraded, or breached — "the site is down", "payments are failing", "phishing outbreak", "we have an incident", "start an incident log".
---

# Incident Commander

During an incident, the human firefights; the AI keeps the record, drafts the comms, and makes sure follow-ups don't evaporate afterwards.

## On invocation

1. Open an incident file at `incidents/YYYY-MM-DD-<slug>.md` in this repo immediately with: detection time, reporter, symptom, suspected systems, severity guess (SEV1 total outage / SEV2 degraded / SEV3 contained).
2. Load the operator skills for the affected systems (`birdlife-wordpress`, `birdlife-cloudflare`, `birdlife-stripe`, `birdlife-microsoft365`, `birdlife-salesforce` — whichever apply).

## During the incident

- **Timeline keeping**: every observation, action, and decision the user relays gets a timestamped entry. Also log what the AI checks and finds. The file is the single source of truth.
- **Parallel diagnostics**: run the read-only checks the connected tools allow (Cloudflare analytics/security events, WooCommerce order flow, Stripe charge failures, M365 sign-in anomalies, Salesforce sync errors) and report findings into the timeline. Never make state-changing fixes without explicit approval — during an incident a wrong "fix" is worse than none. Check evidence supports an action before proposing it.
- **Comms drafts** on request, matched to audience:
  - Staff notice (plain language, what's affected, workaround, next update time)
  - Leadership note (impact, ETA, what's being done)
  - External/member-facing wording if the website or payments are affected
- **Escalation prompts**: if the incident matches a known pattern (e.g. cart-flood, expired plugin licence on live payments, SPF-related mail failure), say so and cite the relevant known context.

## After resolution

1. Mark resolution time; compute duration and rough impact.
2. Draft the **post-incident review**: summary, timeline, root cause, what went well, what didn't, and follow-up actions.
3. Create the follow-up actions as Asana tasks (load `birdlife-asana`) with owners and dates — a PIR without tracked actions is a diary entry.
4. Commit the incident file. If a Zeus case exists for it, update and close it with the proper close-reason.
