Generate the weekly operations report. Run all queries silently, then produce the full report.

## Data to Gather

### Jira
- All bugs by severity (P1, P2, P3, P4) across engineering teams, split by:
  - Production-facing issues
  - Internal/tooling issues
- Bugs opened this week vs. closed this week (net change)
- Any bugs approaching or past SLA:
  - P1: 4 hours
  - P2: 24 hours
  - P3: 72 hours
  - P4: 2 weeks
- Oldest open P1/P2 bugs

### PagerDuty
- Total incidents this week
- Incidents by severity (SEV1, SEV2, SEV3)
- MTTR (mean time to resolve) for the week
- Any currently open incidents
- Teams/services with the most incidents

### Datadog
- Monitors: how many in OK / WARN / ALERT / NO DATA state
- Any SLOs currently below target
- Error rate trends (up/flat/down vs. last week)
- Any notable anomalies this week

## Cross-Reference Analysis
- Any bugs that correlate with PagerDuty incidents (same service, same timeframe)?
- Any SLAs at risk of breach?
- Anything that needs escalation or is a pattern worth flagging?

## Output

Save to `reports/weekly/YYYY-WXX.md` and display:

```markdown
# Weekly Ops Report — Week of [date]

## Summary
[2-3 sentence plain-language summary of the week's health]

## Incidents (PagerDuty)
| Metric | This Week | Last Week |
|---|---|---|
| Total incidents | | |
| SEV1 | | |
| SEV2 | | |
| MTTR | | |
| Currently open | | |

**Top affected services:** [list]

## Bugs (Jira)
| Severity | Open | Opened | Closed | SLA at risk |
|---|---|---|---|---|
| P1 | | | | |
| P2 | | | | |
| P3 | | | | |
| P4 | | | | |

**Oldest open P1/P2:** [ticket ID + age]

## Monitor Health (Datadog)
| State | Count |
|---|---|
| OK | |
| WARN | |
| ALERT | |
| NO DATA | |

**SLOs below target:** [list or "none"]
**Error rate trend:** [up/flat/down vs. last week]

## Escalations & Patterns
[Anything that needs attention, cross-referenced findings, repeated patterns]

## Postmortem status
[Any incidents from this week missing postmortems? Link to Confluence]
```

After saving, confirm the file path and offer to generate a plain-text version suitable for sharing via email or Slack.
