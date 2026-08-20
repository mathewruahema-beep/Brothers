---
name: kb-capture
description: Capture ICT knowledge into a searchable, version-controlled knowledge base — turn a fix that just worked, a decision, a vendor call, or a config change into a written runbook/decision record, so context lives in the ecosystem instead of in one person's head. Use when the user says "write that down", "add to the KB", "document this", "how did we fix this last time", or after any resolved issue worth remembering.
---

# Knowledge Base Capture

Every solved problem is either documented once or re-solved forever. This skill makes documentation a 30-second act instead of a task that never happens.

## Structure (in this repo)

- `kb/runbooks/<slug>.md` — how to do/fix a thing (steps, prerequisites, gotchas)
- `kb/decisions/YYYY-MM-DD-<slug>.md` — why a thing was chosen (context, options, decision, consequences)
- `kb/systems/<system>.md` — living notes per system (quirks, credentials location *by reference only*, vendor contacts, known issues)

## Capture workflow

1. Take whatever the user gives — a sentence, a pasted email thread, the tail of a troubleshooting conversation — and draft the entry in the right category. Runbooks get numbered steps and a "symptoms" section so future searches match; decision records get the context/options/decision/consequences shape.
2. **Never store secrets.** Passwords, keys, tokens: replace with a pointer to where the secret properly lives ("in the password manager under X"). If the user pastes a secret, say so and store the pointer instead.
3. Cross-link: if the entry relates to a Zeus case, Asana task, or incident file, reference it by number/path.
4. Commit with a descriptive message. The git history is the audit trail of when knowledge was added and changed.

## Retrieval workflow ("how did we fix this last time?")

Search `kb/` and `incidents/` (Grep by symptom keywords, not just titles), return the matching runbook with a one-line summary, and ask whether it still worked — if the fix has drifted, update the runbook in the same breath. Stale KB is worse than no KB.

## Proactive nudge

After helping resolve any non-trivial issue in a session where this repo is open, offer once: "Worth a runbook?" — draft it if yes, drop it if no.
