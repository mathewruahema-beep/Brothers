---
name: licence-register
description: Maintain the ICT licence and renewal register — a committed inventory of every SaaS subscription, WordPress plugin licence, domain, certificate and support contract, with renewal dates, owners and costs; AI keeps it current, flags what's expiring, and catches licences that already lapsed. Use when the user says "licence register", "what's expiring", "renewals", "plugin licences", "add a licence", or "review subscriptions".
---

# Licence & Renewal Register

Expired licences on production systems get discovered by outages; this register makes them get discovered by a report instead.

## The register

Lives at `register/licences.yaml` in this repo — one entry per licence/subscription/contract:

```yaml
- name: ""            # product / plugin / service
  vendor: ""
  category: ""        # saas | wp-plugin | domain | certificate | support | infrastructure
  system: ""          # what it protects/powers (e.g. birdlife.org.au, M365 tenant)
  renewal_date: ""    # YYYY-MM-DD
  cost: ""            # amount + currency + cycle (e.g. "USD 199/yr")
  owner: ""           # who holds the account/pays
  criticality: ""     # critical | important | nice-to-have
  status: ""          # active | expiring | EXPIRED | cancelled
  notes: ""
```

If the file doesn't exist yet, offer to seed it: start from the known WordPress plugin inventory (`birdlife-wordpress` — including any already-expired licences on live payment paths, which go in as `EXPIRED`/`critical` immediately), then M365/Salesforce/NetSuite/Asana/Zapier subscriptions, domains and certificates. Fill unknowns with `""` and list them as questions for the user rather than guessing.

## Operations

- **Review** (default): parse the register, report — EXPIRED items first (these are live risk), then expiring within 60 days, then a cost summary by category. Cross-check `wp-plugin` entries against the live plugin list where tools allow, and flag drift (plugin present but not in register, or vice versa).
- **Add/update**: append or edit entries from whatever the user provides (an email, an invoice, a sentence). Normalise dates and costs. Commit with a message naming the change.
- **Renewal actions**: for anything expiring, offer to create an Asana task ("Renew <name> before <date>") and a calendar reminder 2 weeks prior.

## Rules

- The YAML file is the source of truth; always commit after changing it so history shows when each licence was updated and by which conversation.
- Never mark something renewed without the user confirming payment actually happened.
