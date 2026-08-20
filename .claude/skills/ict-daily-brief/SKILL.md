---
name: ict-daily-brief
description: Generate the ICT Manager's morning brief — open Salesforce "Ask Zeus" cases, the Asana IT Operations board, today's calendar, flagged overnight email, and any payment/website incidents — condensed into one prioritised digest with recommended first actions. Use when the user says "daily brief", "morning brief", "what's on today", "start my day", or "catch me up".
---

# ICT Daily Brief

Produce a single prioritised digest so the ICT Manager starts the day with full context instead of opening five systems.

## Data to gather (run in parallel where possible)

1. **Helpdesk queue (Salesforce "Zeus")** — load the `birdlife-salesforce` and `birdlife-ict-assistant` skills for the Case model, then query open Cases: status, age, requester, subject. Flag:
   - Cases older than 5 business days
   - Anything mentioning phishing, compromise, MFA, or payment failure (treat as priority)
   - New cases since yesterday
2. **Asana IT Operations Project Plan** — load `birdlife-asana`, then pull tasks assigned to the user plus anything in Blocked. Flag items due today/overdue.
3. **Calendar** — today's meetings (Google Calendar or Outlook, whichever responds). Note gaps usable for deep work.
4. **Email** — search unread/flagged messages from the last 18 hours in the connected mailbox. Surface only things needing a decision or reply from the ICT Manager; ignore newsletters and automated notices unless they signal an outage.
5. **Systems pulse (best effort, don't block the brief on these)**:
   - Stripe/WooCommerce: any failed payments, disputes, or refund anomalies overnight (`birdlife-stripe`, `birdlife-wordpress`)
   - Cloudflare: unusual traffic or security events if quickly checkable (`birdlife-cloudflare`)

## Output format

A short digest, most urgent first:

1. **Top 3 actions today** — one line each, with why
2. **Helpdesk** — counts (new / open / aging), then only the cases worth attention with a one-line AI summary each
3. **Projects & tasks** — due/overdue/blocked from Asana
4. **Schedule** — meetings + suggested focus block
5. **Inbox** — items needing a reply, each with a suggested one-line response angle
6. **Systems pulse** — one line per system; "all quiet" is a valid line

Keep the whole brief readable in under two minutes. Offer to act on any item (draft the reply, move the task, triage the case) — don't act without being asked.
