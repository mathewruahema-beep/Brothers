---
name: zeus-triage
description: AI triage of the Salesforce "Ask Zeus" helpdesk queue — categorise every open case, set priority, draft requester replies, propose owner (self vs Keith vs vendor), and sync actionable work into Asana. Use when the user says "triage the queue", "triage zeus", "work the tickets", or "clear the helpdesk backlog".
---

# Zeus Queue Triage

Turn a raw helpdesk queue into a categorised, prioritised work plan with drafted replies — the human approves, the AI does the legwork.

## Prerequisites

Load `birdlife-salesforce` and `birdlife-ict-assistant` first — they carry the real Case statuses, the mandatory close-reason field, and the exact line between what can be changed directly and what needs Entra admin access. Load `birdlife-asana` if syncing tasks.

## Workflow

1. **Pull the queue**: all Cases not closed, oldest first. Include subject, description, requester, status, age, last activity.
2. **Categorise each case** into one of:
   - `access` (MFA, password, licence, mailbox, distribution list, permissions)
   - `hardware/device`
   - `software/app` (M365, Salesforce, NetSuite, WordPress, etc.)
   - `security` (phishing, suspicious sign-in, compromise) — always highest priority
   - `request` (new starter, offboarding, procurement)
   - `question/how-to`
3. **Assess each case**:
   - Priority (P1 outage/security → P4 convenience), with one-line justification
   - Can it be resolved directly with current access, or is it blocked on Entra admin / vendor / third party? Say which.
   - Is it a duplicate of another open case? Link them.
   - Quick wins: cases resolvable in under 10 minutes get tagged `quick-win`.
4. **Draft replies**: for every case needing requester communication, draft the reply in plain, friendly language (BirdLife staff are largely non-technical). Never send without approval.
5. **Sync to Asana** (on request): cases that represent real work (not one-line answers) become tasks on the IT Operations Project Plan in the right section, linked back to the Case number.
6. **Stale-case sweep**: cases with no activity for 10+ days → propose a nudge reply or closure with the mandatory close-reason.

## Output format

A triage table: Case # | Age | Category | Priority | Recommendation (one line). Below it: quick wins first, then drafted replies grouped by case, then the list of proposed Asana tasks and proposed closures. Ask once for approval, then execute all approved actions in bulk.
