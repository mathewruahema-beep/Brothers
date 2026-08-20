# ICT Manager Toolkit

AI-powered working tools for the BirdLife Australia ICT Manager, built as Claude Code skills. Open this repository in Claude Code (web, desktop, or CLI) and the skills load automatically — invoke them by name (e.g. `/zeus-triage`) or just describe what you need in plain language and the matching skill triggers.

The toolkit is built on one principle: **context stays in the digital ecosystem** — helpdesk state in Salesforce, work in Asana, knowledge and history in this git repository — never only in one person's head or inbox.

## The tools

| Tool | Invoke with | What it does |
|---|---|---|
| **ICT Daily Brief** | `/ict-daily-brief`, "catch me up" | One prioritised morning digest: Zeus cases, Asana board, calendar, flagged email, systems pulse, top 3 actions. |
| **Zeus Triage** | `/zeus-triage`, "triage the queue" | AI categorises and prioritises every open helpdesk case, drafts requester replies, flags quick wins and stale cases, syncs real work to Asana. |
| **Starter / Leaver** | `/starter-leaver`, "onboard Jane" | Runs the full onboarding/offboarding runbook — executes what current access allows, generates exact admin steps for the rest, tracks it all as an Asana checklist. |
| **Meeting → Actions** | `/meeting-actions`, paste notes | Extracts decisions and actions from meeting notes/transcripts, creates owned + dated Asana tasks, drafts the follow-up email, checks last meeting's carry-overs. |
| **Weekly ICT Report** | `/weekly-ict-report` | Management-ready status report assembled from live Salesforce + Asana data: metrics, project status, incidents, security, next week. Saved to `reports/` for week-on-week trends. |
| **Incident Commander** | `/incident-log`, "the site is down" | Keeps a timestamped incident timeline, runs read-only diagnostics across systems, drafts stakeholder comms, produces the post-incident review with tracked follow-ups. |
| **Reconciliation Watch** | `/recon-watch` | Cross-checks Stripe ↔ WooCommerce ↔ Salesforce ↔ NetSuite for a date range; classifies every mismatch and turns exception clusters into tracked work. Read-only on money. |
| **Licence Register** | `/licence-register`, "what's expiring" | Version-controlled inventory of every licence, plugin, domain, cert and contract in `register/licences.yaml`; flags expiring and already-expired items before they become outages. |
| **KB Capture** | `/kb-capture`, "write that down" | Turns fixes, decisions and system quirks into searchable runbooks and decision records in `kb/` — and retrieves them when the same problem returns. |

## Zeus Field Kit (`index.html`)

A single-page remote ICT management hub — the clickable companion to the
skills above, built mobile-first for working while travelling. Open
`index.html` in any browser: it is fully self-contained (no build step, no
server, no dependencies beyond Google Fonts) and works offline apart from
the fonts.

On the page: one-tap links into every admin console (Salesforce, Asana,
M365/Entra/Exchange/Defender/Intune, Cloudflare, WP Engine, WordPress,
Stripe, NetSuite, Zapier), runbooks for the common jobs with the traps
marked (case close-reason validation, onboarding, offboarding, MFA resets,
phishing triage, website incidents), and escalation contacts. A search box
live-filters everything.

This public copy is the generic edition. The full edition — with internal
reference IDs and the operational watchlist — lives privately.

Everything lives in plain markup — when a value on the page disagrees with
the live console, trust the console and fix the page.

## Repository layout

```
.claude/skills/     the nine tools (one folder per skill)
index.html          Zeus Field Kit — the remote ops hub page
reports/            weekly reports and recon runs (accumulates history)
incidents/          incident timelines and post-incident reviews
kb/                 runbooks, decision records, per-system notes
register/           licences.yaml — the renewal register
```

The `reports/`, `incidents/`, `kb/` and `register/` directories are created by the tools as they run; everything they produce is committed, so the repository becomes the ICT team's institutional memory with full history.

## Why this design

- **AI does the legwork, the human approves.** Every tool drafts, categorises, cross-checks and summarises — but replies aren't sent, cases aren't closed, and money is never touched without explicit approval.
- **Everything lands in a system of record.** Actions become Asana tasks, ticket work stays in Salesforce, knowledge and reports live in git. Nothing important ends its life in a chat window.
- **Safe by default.** Financial and security-relevant operations are read-only; secrets are never stored (pointers only); state-changing fixes during incidents require sign-off.
- **Compounding value.** Because outputs are committed, week-on-week helpdesk trends, recurring incident patterns, and "how did we fix this last time" all get cheaper to answer every week.

## Requirements

Claude Code with the BirdLife connectors enabled (Salesforce, Asana, Microsoft 365, NetSuite, Gmail/Google Calendar, Cloudflare, Zapier). The tools lean on the account-level `birdlife-*` operator skills for system-specific knowledge — keep those enabled.
