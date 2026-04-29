Run this at end of day. Auto-ingest today's daily note first, then gather context, then prompt.

## Step 0: Auto-ingest today's daily note

Check if `wiki/daily/YYYY-MM-DD.md` exists (today's date).
Check `wiki/log.md` — was it already ingested today?

If it exists and has NOT been ingested yet:
- Read the daily note
- Extract every meeting block — who attended, what was discussed, decisions, commitments
- Update or create `wiki/people/[Name].md` for every person named (see WIKI.md for page structure)
- Extract `- [ ]` action items → append to `inbox.md` as `- [ ] [item] — from [date]`
- Extract significant decisions → create `decisions/YYYY-MM-DD-[topic].md` if warranted
- Extract recurring themes/frameworks → update `wiki/concepts/` if a pattern is emerging
- Append to `wiki/log.md`: `## [date] ingest-daily | Processed [date] note: [N meetings, N people, N actions]`
- Update `wiki/index.md` with any new/modified pages
- Overwrite `wiki/hot.md` entirely with updated state

If no daily note exists or it was already ingested, skip Step 0 silently.

---

## Step 1: Silent Context Gathering

Before prompting, check (with wiki context now loaded from Step 0):
- PagerDuty: any incidents today I was involved in?
- Jira: any tickets I closed or moved to done today?
- `decisions/`: any new files created today?
- `reports/daily/`: what did I say I was going to do today (from this morning's report)?
- `wiki/hot.md`: who did I meet with today, what commitments were made?

## Step 2: Smart Prompt

Based on what you found, ask 3-5 targeted questions. Examples (adapt based on context):

- "I see there was a PagerDuty incident this afternoon — were you involved in the response? Worth capturing."
- "You closed [ticket X] today — was that the full fix or is there follow-up work?"
- "You mentioned [thing from morning] as your one thing — how did that go?"
- "I see you met with [Name] today — anything from that conversation worth adding beyond the notes?" (only if daily note was ingested and person is known)
- "Did you have any conversations today that aren't in your daily note but worth capturing?"
- "Any wins today — shipping something, unblocking someone, a good decision made?"
- "Anything still open in your head that you want to get out before logging off?"

Always end with: "Anything else before you close the laptop?"

## Step 3: Process the Response

From the user's answers:

**Inbox** — Append any action items to `inbox.md` as checkboxes:
```
- [ ] [action item] — added [date]
```

**Bragdoc** — Append wins to `bragdoc/YYYY-MM-DD.md` (create if doesn't exist):
```
## [Date]
- [win 1]
- [win 2]
```

**Daily report** — Save summary to `reports/daily/YYYY-MM-DD.md`:
```
## EOD — [Date]

### Done today
- [completed items]

### Open loops
- [things still in flight]

### Action items for tomorrow
- [ ] [item]

### Wins
- [wins]

### Notes
[anything else worth remembering]
```

## Step 4: Close

Confirm what was saved and where. Keep it brief. Something like:
"Captured [N] action items to inbox, [N] wins to bragdoc. See you tomorrow."
