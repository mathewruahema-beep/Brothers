---
name: weekly-ict-report
description: Generate the weekly ICT status report for management — helpdesk metrics from Salesforce, project progress from Asana, incidents, security posture notes, and next week's focus — written by AI from live system data, delivered as a polished document or email draft. Use when the user says "weekly report", "status report", "management update", or "what did we do this week".
---

# Weekly ICT Report

A management-ready report assembled from live data, not memory — takes minutes, not an afternoon.

## Data to gather

Load `birdlife-salesforce`, `birdlife-asana`, and any system skills relevant to the week's incidents.

1. **Helpdesk (Zeus)**: cases opened/closed/still open this week, average age, oldest case, category breakdown, notable resolutions.
2. **Projects (Asana IT Operations Project Plan)**: tasks completed this week, moved to Blocked (with reasons), newly added, and % progress on major initiatives (e.g. membership rebuild, Better Impact, BC migration business case — whatever is live on the board).
3. **Incidents & changes**: anything the user flags plus what's visible in the systems (site incidents, payment anomalies, security events). One paragraph each: what happened, impact, resolution, follow-up.
4. **Security posture**: MFA/Conditional Access remediation progress, phishing reports handled, Essential Eight items touched (from `birdlife-microsoft365` context and the week's cases).
5. **Next week**: due tasks, scheduled changes, known risks.

## Output

Structure:

1. **Executive summary** — 3-4 sentences a non-technical exec can read: what was delivered, what's at risk, what's needed from them (if anything).
2. **Helpdesk metrics** — small table, week-on-week comparison if last week's report exists in the repo (`reports/` directory).
3. **Project progress** — per-initiative one-liners with status (On track / At risk / Blocked).
4. **Incidents** — or "No incidents this week."
5. **Security** — brief.
6. **Next week's focus** — max 5 bullets.

Save the report to `reports/YYYY-MM-DD-weekly-ict-report.md` in this repo and commit it, so history accumulates and week-on-week trends become possible. Then offer: an email draft to the leadership distribution, and/or a formatted Word document via the docx skill.

Write plainly. Numbers over adjectives. Flag risks honestly — the report's value is that management trusts it.
