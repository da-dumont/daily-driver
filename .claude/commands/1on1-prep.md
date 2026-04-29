Prepare for a 1:1 meeting with a specific person, drawing on their full wiki history.

Usage: /1on1-prep [name]

## Steps

**1. Read wiki/hot.md**
Check for any recent activity on this person — meetings, open items, or threads from the last few sessions.

**2. Read wiki/people/[name].md**
Load their full page: overview, growth arc, patterns, meeting log, open items.
If no page exists yet: create a stub page with basic frontmatter, then continue.

```yaml
---
type: person
title: "[Name]"
created: [today]
updated: [today]
tags: []
status: seed
related: []
role: ""
team: ""
direct_report: false
last_meeting: null
meeting_count: 0
---

# [Name]

## Overview
[To be filled in as meetings are logged]

## Growth arc
[For direct reports — to be developed over time]

## Patterns
[To be developed over time]

## Meeting log

## Open items
```

**3. Query Jira (if direct report)**
Pull their recent ticket activity — what they've closed, what's in progress, anything overdue.

**4. Synthesize briefing**

Output structured as:

```
## 1:1 Prep — [Name] — [today's date]

### Follow-up items
[Open commitments from last meeting — yours and theirs. Flag anything overdue.]

### What they likely want to discuss
[Based on patterns, recent activity, what's been on their mind across recent meetings]

### Development thread
[For direct reports: where are they in their growth arc, what's the conversation to advance]

### One thing to listen for
[A pattern, tension, or signal worth being attuned to based on history]

### Jira pulse (if direct report)
[Recent ticket activity summary]
```

**5. After the meeting**

Prompt: "How did the 1:1 go? 2-3 sentences to log."

Take the response and:
- Append a new entry to their meeting log in `wiki/people/[name].md`:
  ```
  ### [Date] — 1:1
  [Summary of what was discussed, decisions, commitments]
  - Me: [commitment]
  - Them: [commitment]
  ```
- Update **Open items** — close anything resolved, add new commitments
- Update `last_meeting` and increment `meeting_count` in frontmatter
- Update `wiki/index.md` entry for this person
- Append to `wiki/log.md`: `## [date] 1on1-prep | [Name] — prep generated, post-meeting summary logged`
- Overwrite `wiki/hot.md` with updated state
