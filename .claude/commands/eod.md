Run this at end of day. Gather context silently first, then prompt — don't ask a wall of questions upfront.

## Step 1: Silent Context Gathering

Before prompting, check:
- PagerDuty: any incidents today I was involved in?
- Jira: any tickets I closed or moved to done today?
- `decisions/`: any new files created today?
- `reports/daily/`: what did I say I was going to do today (from this morning's report)?

## Step 2: Smart Prompt

Based on what you found, ask 3-5 targeted questions. Examples (adapt based on context):

- "I see there was a PagerDuty incident this afternoon — were you involved in the response? Worth capturing."
- "You closed [ticket X] today — was that the full fix or is there follow-up work?"
- "You mentioned [thing from morning] as your one thing — how did that go?"
- "Did you have any 1:1s or significant conversations today that are worth capturing?"
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
