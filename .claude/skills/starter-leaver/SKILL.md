---
name: starter-leaver
description: Run the onboarding (new starter) or offboarding (leaver) runbook end-to-end — build the checklist, execute every step possible with current access across M365/Entra, Salesforce, Asana and other SaaS, generate the exact admin actions for steps needing elevated access, and track the whole thing as an Asana task with subtasks. Use when the user says "new starter", "onboard", "offboard", "someone is leaving", or names a person joining/departing.
---

# Starter / Leaver Runbook

One command runs the whole joiner or leaver process, so nothing is forgotten and every step is evidenced.

## Prerequisites

Load `birdlife-microsoft365` (Entra/M365 process, Employment Hero sync, what needs admin access), `birdlife-ict-assistant` (the can-do vs needs-Entra-admin line), `birdlife-asana`, and `birdlife-salesforce` (licence/user handling in Zeus).

## Inputs to collect (ask once, up front)

Name, start/end date, role and team, manager, and for starters: licence tier, required group/DL memberships, shared mailbox access, and whether they need Salesforce, NetSuite, Asana, or WordPress accounts.

## Onboarding checklist (generate + execute)

1. Entra ID account (via Employment Hero sync where applicable — verify it arrived; note anything requiring manual admin action)
2. Licence assignment (M365 tier per role)
3. Group and distribution list memberships
4. Shared mailbox access
5. SaaS accounts as needed: Salesforce, Asana, NetSuite, others
6. Device/Intune enrolment note for the hardware step
7. Welcome email draft to the starter's manager: what's done, what they must do (MFA setup on day one, etc.)

## Offboarding checklist (generate + execute)

1. Disable sign-in / revoke sessions (flag if it needs Entra admin — output the exact steps)
2. Remove licences, groups, DLs
3. Mailbox: convert to shared / set delegate per manager's choice
4. OneDrive/SharePoint ownership transfer
5. Deactivate SaaS accounts: Salesforce, Asana, NetSuite, WordPress (check for the self-registration flaw accounts), Zapier connections owned by the leaver
6. Recover device; note any personal MFA methods to strip
7. Confirmation summary email draft to HR/manager

## Execution rules

- Create one Asana task "Onboard/Offboard <name>" on the IT Operations Project Plan with each checklist item as a subtask; tick them off as they complete.
- Execute directly what current access allows; for everything else, output a copy-paste-ready admin action list (exact portal path or PowerShell) instead of silently skipping.
- Finish with a status table: Done / Needs admin / Waiting on third party, so the audit trail lives in Asana, not in someone's head.
