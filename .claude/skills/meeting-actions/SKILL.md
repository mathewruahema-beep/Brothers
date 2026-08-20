---
name: meeting-actions
description: Turn meeting notes, a transcript, or a recording summary into tracked work — extract decisions and action items with AI, create Asana tasks with owners and due dates, draft the follow-up email, and file the summary. Use when the user pastes meeting notes, mentions a meeting that just happened, or says "capture actions", "minutes", or "follow up from the meeting".
---

# Meeting → Actions

Meetings leak context; this skill captures it into the digital ecosystem the moment the meeting ends.

## Sources (in order of preference)

1. Notes/transcript pasted by the user
2. Zoom or Granola meeting assets if connected (search by meeting title/date)
3. A calendar event's description + the user's verbal recap

## Workflow

1. **Extract** with clear separation:
   - **Decisions** (things agreed — record verbatim intent, not paraphrase)
   - **Actions** (verb + owner + due date; infer a sensible due date if none was stated and mark it as inferred)
   - **Risks/parking lot** (raised but unresolved)
2. **Confirm the action list** in one compact table before creating anything.
3. **Create Asana tasks** (load `birdlife-asana`): one task per action on the appropriate project — IT Operations Project Plan by default — with the meeting name and date in the description, assignee where the owner is an Asana user, and due date set. Actions owned by non-Asana people go into the follow-up email instead.
4. **Draft the follow-up email**: decisions, actions with owners/dates, and risks — short enough that people actually read it. Leave it as a draft for the user to send.
5. **File the summary**: append/attach the structured summary where the user keeps meeting records (Asana task comment, SharePoint, or Google Drive doc — follow the user's stated preference and remember it in-session).

## Rules

- Never invent an owner. Unowned actions get flagged "owner needed" and go to the user.
- Recurring meetings: check for the previous instance's open actions and report which are still open — carry-overs are where follow-through dies.
