# Wiki — Schema & Operational Guidelines

This is the LLM wiki for Dan Dumont's daily driver. Claude writes and maintains all pages in this wiki. You (Dan) write only in `wiki/daily/`. Everything else is compiled by Claude automatically.

---

## How it works

**You write** in `wiki/daily/YYYY-MM-DD.md` during and after meetings.
**Claude compiles** your notes into structured pages — people, concepts, research, decisions.
**You browse** the results in Obsidian — graph view, search, linked pages.
**Hot cache** (`wiki/hot.md`) keeps Claude oriented across sessions without re-reading everything.

---

## Hot cache rules (critical)

- `wiki/hot.md` is always read first — at session start and before any wiki query
- After every wiki write operation, **overwrite hot.md entirely** — never append
- Keep it under ~500 words
- It contains: recent people activity, active research threads, recent decisions, open commitments, last daily note processed

---

## Tiered reading order

1. `wiki/hot.md` — recent context (~500 tokens, answers most recent questions)
2. `wiki/index.md` — find relevant pages (~1000 tokens)
3. Individual pages — drill in as needed (100–300 tokens each)

Never load the full wiki. Always start with hot.md.

---

## Directory structure

| Path | What it is | Who writes it |
|---|---|---|
| `wiki/daily/` | Raw capture — Obsidian Daily Notes | You |
| `wiki/people/` | One page per person, compounds over time | Claude |
| `wiki/research/` | Deep dives on topics | Claude |
| `wiki/concepts/` | Frameworks, mental models, recurring themes | Claude |
| `wiki/sources/` | Summary pages for ingested articles/docs | Claude |
| `wiki/questions/` | Filed answers to queries worth keeping | Claude |
| `wiki/hot.md` | Hot cache — always read first, always overwritten | Claude |
| `wiki/index.md` | Master catalog of all pages | Claude |
| `wiki/log.md` | Append-only operation log (newest at top) | Claude |
| `wiki/overview.md` | Executive summary of the entire wiki | Claude |

---

## Page schema

Every wiki page uses YAML frontmatter:

```yaml
---
type: person|research|concept|source|question|meta
title: "Human-Readable Title"
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
status: seed|developing|mature
related:
  - "[[Other Page]]"
---
```

### People pages — additional fields

```yaml
role: "Their title"
team: "Their team"
direct_report: true|false
last_meeting: YYYY-MM-DD
meeting_count: N
```

People page content structure:
1. **Overview** — role, relationship, one-line characterization
2. **Growth arc** — development themes, what they're working toward (for directs)
3. **Patterns** — what energizes/frustrates them, communication style, recurring themes
4. **Meeting log** — chronological entries newest first: date, type, key topics, decisions, commitments
5. **Open items** — unresolved commitments and follow-ups

---

## Daily note ingest rules

When Claude processes a `wiki/daily/YYYY-MM-DD.md`:

1. Extract every meeting and note block
2. For each person named: update or create `wiki/people/[Name].md`
3. Extract action items → append to `inbox.md` as `- [ ] [item] — from [date]`
4. Extract significant decisions → create or update `decisions/YYYY-MM-DD-[topic].md`
5. Extract recurring themes or frameworks → update `wiki/concepts/`
6. Append ingest entry to `wiki/log.md` (newest at top)
7. Update `wiki/index.md` with all modified pages
8. Overwrite `wiki/hot.md`

**Signal patterns Claude looks for:**
- `## 1:1 [Name]` → person page update
- `## [Meeting name] / **Attendees:**` → multi-person update
- `**Decisions**` / `**Commitments**` → file to person pages and decisions/
- `- [ ]` → action item for inbox.md
- `## Reading:` / `**Source:**` → source page in wiki/sources/
- `## Note —` → freeform, extract names and actions

---

## Note capture templates

Use these in your daily note. Write naturally — the headers are the extraction signal, not a rigid form.

---

### 1:1 meeting

```
## 1:1 [Name] — [time]

**Their agenda**
[What they brought up]

**My agenda**
[What I wanted to cover]

**Key discussion**
[What actually mattered in the conversation]

**Commitments**
- Me: [what I said I'd do]
- Them: [what they said they'd do]

**Notes / observations**
[Anything worth remembering — how they're doing, what's on their mind, patterns]
```

---

### Strategy or planning meeting

```
## [Meeting name] — [time]
**Attendees:** [names]

**Context**
[What this meeting was about / why it was called]

**Key discussion**
[Main points, debates, perspectives raised]

**Decisions**
- [Decision made, who owns it]

**Open questions**
- [Things left unresolved]

**Actions**
- [ ] [Owner]: [action item]
```

---

### Team or all-hands meeting

```
## [Meeting name] — [time]
**Attendees:** [team or list]

**Topics covered**
[High-level summary]

**Signals / patterns**
[Team energy, recurring themes, concerns surfaced]

**Follow-ups**
- [ ] [action item]
```

---

### Async / informal note

```
## Note — [topic or person]

[Freeform. Include names, decisions, or actions.]
```

---

### Research / reading note

```
## Reading: [Title]
**Source:** [URL or filename]

[Key points, your reactions, what's relevant to current work]
```

---

## Log format

Each entry in `wiki/log.md` starts with a consistent prefix for easy parsing:

```
## [YYYY-MM-DD] [operation] | [description]
```

Examples:
```
## [2026-05-01] ingest-daily | Processed daily note: 2 1:1s, 1 strategy meeting, 4 action items
## [2026-05-01] 1on1-prep | Brooks — generated prep, logged post-meeting summary
## [2026-04-30] ingest-source | Article: "How to structure platform teams"
```

---

## Index format

Each entry in `wiki/index.md`:

```
- [[Page Title]] — one-line summary (type: person|concept|research|source) updated: YYYY-MM-DD
```

Organized by section: People, Concepts, Research, Sources, Questions.

---

## Lint checks (run periodically)

Ask Claude to "lint the wiki" to find:
- Orphan pages with no inbound links
- Open items older than 30 days with no update
- People mentioned in daily notes without a wiki page
- Concepts mentioned repeatedly without a concept page
- Stale research threads with no activity in 60+ days
