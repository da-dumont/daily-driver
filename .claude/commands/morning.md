Run the following steps silently in sequence, then produce a single structured briefing.

## Steps

1. **Yesterday's notes** — Read the most recent file in `reports/daily/`. If none exists, skip.

2. **Jira queue** — Query Jira for:
   - Tickets assigned to me that are overdue or due today
   - Any P1/P2 bugs opened in the last 24 hours across my teams
   - Tickets I'm watching that have had recent activity

3. **PagerDuty** — Query for:
   - Any incidents that triggered since yesterday EOD
   - Currently open incidents
   - On-call handoffs today

4. **Datadog** — Query for:
   - Any monitors in ALERT or WARN state
   - SLO breach risk (anything <99% over last 7 days)

5. **Process yesterday's daily note (safety net)**
Check `wiki/log.md` — was yesterday's daily note (`wiki/daily/YYYY-MM-DD.md` for yesterday) already ingested?

If NOT ingested:
- Run the same ingest flow as /eod Step 0 on yesterday's note
- Update people pages, inbox, decisions, concepts as needed
- Update wiki/log.md, wiki/index.md, overwrite wiki/hot.md

If already ingested:
- Read `wiki/hot.md` and surface any active threads or open items relevant to today
  (people you're meeting today who have open commitments, active research threads, etc.)

6. **Day-of-week nudge** — Check today's day against the schedule in CLAUDE.md and include the relevant focus reminder.

## Output Format

```
## Good morning — [Day, Date]

### Yesterday's thread
[1-3 bullets from EOD notes — open loops, things to follow up]

### Overnight
[PagerDuty incidents, Datadog alerts — or "All clear" if none]

### Jira queue
[Overdue / due today / P1-P2 new bugs]

### Wiki threads
[Active research threads or open commitments from wiki/hot.md relevant to today — or omit if nothing relevant]

### Today's focus
[Day-of-week nudge from CLAUDE.md]

### One thing
[Single highest-leverage action to do before anything else, based on all of the above]
```

Keep the briefing scannable. No walls of text. Flag anything that needs immediate attention at the top with ⚠️.
