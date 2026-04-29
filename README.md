# Daily Driver

A persistent Claude Code workspace for engineering leaders. Not a one-off AI session — an operating environment that accumulates context, connects to your tools, and gets better the more you use it.

Built for a Director of Engineering, but adaptable to any engineering leadership role.

---

## What this is

Most AI interactions start cold. You open a session, do a thing, close it, and all context disappears.

A daily driver is different. It's a workspace with memory (via files), opinions (via encoded roles), and live data (via integrations). You open Claude Code here in the morning and drive your entire day from it — briefings, task management, drafting, decision support, incident response, and more.

The core insight: when you connect your tools, encode how you think, and let context accumulate over time, the whole becomes greater than the sum of its parts. Information has a lifecycle. Things don't fall through the cracks. Invisible work gets captured. The cognitive load of remembering, tracking, and connecting gets offloaded to something that's more consistent at it than you are.

There are two compounding layers:

- **Operational layer** — live data from Jira, PagerDuty, and Datadog. Daily briefings, triage, weekly ops reports. What's happening now.
- **Knowledge layer** — an LLM-maintained wiki in `wiki/`. Every meeting you write up in Obsidian gets automatically compiled into structured pages: people you've met with, decisions made, themes that recur. It gets richer with every session without extra work from you.

---

## Prerequisites

- [Claude Code](https://claude.ai/code) installed and authenticated
- [Obsidian](https://obsidian.md) (free) — for writing and browsing your wiki
- API access to:
  - **Atlassian** (Jira + Confluence) — one token covers both
  - **Datadog** — API key + App key
  - **PagerDuty** — API token
- See [MCP Setup](#mcp-setup) for where to get each

> Swapping tools? See [Adapting for your org](#adapting-for-your-org).

---

## Getting started

```bash
git clone git@github.com:da-dumont/daily-driver.git
cd daily-driver
```

### 1. Configure integrations
Fill in `.mcp.json` with your API credentials (see [MCP Setup](#mcp-setup)).

### 2. Personalize your context
- `context/team-roster.md` — your team structure
- `context/writing-style.md` — your voice and tone preferences
- `context/principles.md` — leadership frameworks you want Claude to apply

### 3. Set up Obsidian for the wiki
Open Obsidian → Manage Vaults → Open folder as vault → select `daily-driver/wiki/`

Then configure Daily Notes + Templater (see [Wiki setup](#wiki-setup)).

### 4. Start Claude Code
```bash
claude
```

Claude reads `CLAUDE.md` on every session and orients itself. Run `/morning` to begin.

---

## Workspace structure

```
daily-driver/
├── CLAUDE.md                   # Central config — roles, workflows, integrations
├── .mcp.json                   # Integration credentials (gitignored)
├── inbox.md                    # Quick capture buffer
├── context/                    # Reference material Claude uses across all sessions
│   ├── team-roster.md          # Your team structure
│   ├── writing-style.md        # Voice and tone preferences
│   ├── principles.md           # Leadership mental models
│   └── working-with-me.md      # Shareable doc for new colleagues
├── decisions/                  # Permanent record of significant decisions
├── bragdoc/                    # Running log of wins by date
├── reports/
│   ├── daily/                  # EOD summaries (one per day)
│   └── weekly/                 # Weekly ops reports
├── wiki/                       # LLM-maintained knowledge base (browse in Obsidian)
│   ├── WIKI.md                 # Schema, conventions, ingest rules
│   ├── hot.md                  # Hot cache — Claude reads this first every session
│   ├── index.md                # Master catalog of all wiki pages
│   ├── log.md                  # Append-only operation log
│   ├── daily/                  # YOUR Obsidian Daily Notes (raw capture)
│   ├── people/                 # One page per person — compounds with every meeting
│   ├── concepts/               # Frameworks, mental models, recurring themes
│   ├── research/               # Deep dives that accumulate over time
│   ├── sources/                # Ingested articles and documents
│   ├── questions/              # Filed answers worth keeping
│   └── _templates/
│       └── daily-note.md       # Obsidian daily note template
└── .claude/
    └── commands/               # Slash command definitions
        ├── morning.md
        ├── eod.md
        ├── triage.md
        ├── weekly-ops.md
        └── 1on1-prep.md
```

### `CLAUDE.md`

The brain of the workspace. Claude reads this at the start of every session. It defines:
- All 11 roles and their trigger phrases
- Integration behavior
- Day-of-week schedule
- Working principles
- Slash command index

Edit this as your workflow evolves. It's your most important file.

### `inbox.md`

A capture buffer — not a todo list. Put anything here: half-formed thoughts, action items, things you don't want to forget. Raw and unstructured is fine. Process it with `/triage` when it gets noisy. Never work directly from inbox; that's what Jira is for.

### `context/`

Reference material that persists across sessions. Claude reads these files when they're relevant to what you're working on.

| File | What it's for | Used by |
|---|---|---|
| `team-roster.md` | Who's on your team, their roles, notes | [Coach], [Interviewer] |
| `writing-style.md` | Voice, tone, format preferences | [Editor] |
| `principles.md` | Leadership mental models and frameworks | [Founder] |
| `working-with-me.md` | Shareable doc for new colleagues | [Editor] |
| `resume.md` | Career history for self-eval and bragdoc | [EA], bragdoc |

Add any reference file you want Claude to know about. Drop in meeting notes, org charts, competitor analyses, product specs. The more context lives here, the better the responses.

### `decisions/`

A permanent record of significant decisions with rationale. One file per decision, named `YYYY-MM-DD-topic.md`. Populated manually or automatically via `/triage` when you mention a decision in your inbox.

Claude references these in strategic conversations. Over time this becomes a searchable record of how and why you've made calls — useful for onboarding new team members, revisiting past choices, and building your own decision-making track record.

Example files:
```
decisions/2026-05-01-platform-rewrite-scope.md
decisions/2026-05-15-team-structure-q3.md
```

### `bragdoc/`

A running log of wins — things you shipped, problems you solved, people you developed. Populated automatically by `/eod`. Wins fade fast; this is the system that catches them before they do.

Each file is dated: `bragdoc/YYYY-MM-DD.md`. At performance review time or when updating your resume, this is where you go.

### `reports/`

Automatically generated reports from slash commands.

- `reports/daily/YYYY-MM-DD.md` — end-of-day summary: what you did, open loops, tomorrow's action items. Created by `/eod`, surfaced by `/morning`.
- `reports/weekly/YYYY-WXX.md` — full ops report with bug counts, incident data, and monitor health across all integrations. Created by `/weekly-ops`.

You never write these files manually — they're output from your workflows.

### `.claude/commands/`

Slash command definitions. Each file is a prompt that tells Claude exactly what to do when you run that command. You can edit these to change the behavior, add new integrations, or adjust the output format.

---

## Wiki

The `wiki/` directory is a persistent, LLM-maintained knowledge base that compounds over time. It's the second brain of the daily driver.

**The core idea:** instead of re-reading raw notes every time you need context, Claude compiles your daily meeting notes into structured, interlinked pages. Ask about a person and Claude reads their page — every meeting, every commitment, every pattern — not just today's notes. The knowledge accumulates and cross-references automatically.

**How it works:**

- You write meeting notes in Obsidian's Daily Note (`wiki/daily/YYYY-MM-DD.md`) during or after meetings
- `/eod` automatically ingests today's note before asking you anything — updating person pages, filing decisions, extracting action items
- `/morning` ingests yesterday's note as a safety net if `/eod` was skipped
- You never have to remember to run an ingest command

**Hot cache:** `wiki/hot.md` is a ~500-word summary Claude overwrites after every wiki operation. It's always read first — recent people activity, active research threads, open commitments. This keeps Claude oriented across sessions without loading the full wiki every time.

**What the wiki produces automatically:**

| Directory | What goes there | How |
|---|---|---|
| `wiki/people/` | One page per person — meeting log, patterns, open commitments | Auto from daily notes |
| `wiki/concepts/` | Frameworks and mental models that recur across meetings | Auto from daily notes |
| `wiki/research/` | Deep dives on topics you're tracking over time | `/ingest` or auto |
| `wiki/sources/` | Summaries of articles, docs, reports you've read | `/ingest` |
| `wiki/questions/` | Answers to queries worth filing permanently | On demand |

**Browsing:** Open Obsidian with `wiki/` as the vault. Graph view shows how people, decisions, and concepts link to each other. You read; Claude writes.

See `wiki/WIKI.md` for the full schema, frontmatter conventions, and ingest rules.

### Note capture templates

The daily note template (`wiki/_templates/daily-note.md`) pre-loads five capture formats. Write naturally — the headers are what Claude uses as extraction signals.

**1:1 meeting**
```
## 1:1 [Name] — [time]

**Their agenda**
**My agenda**
**Key discussion**
**Commitments**
- Me:
- Them:
**Notes / observations**
```

**Strategy or planning meeting**
```
## [Meeting name] — [time]
**Attendees:** [names]

**Context**
**Key discussion**
**Decisions**
- [decision, owner]
**Open questions**
**Actions**
- [ ] [Owner]: [item]
```

**Team or all-hands meeting**
```
## [Meeting name] — [time]
**Attendees:** [team or list]

**Topics covered**
**Signals / patterns**
**Follow-ups**
- [ ] [item]
```

**Async / informal note** (hallway conversation, Slack thread, quick observation)
```
## Note — [topic or person]

[Freeform. Include names, decisions, or actions.]
```

**Research / reading note**
```
## Reading: [Title]
**Source:** [URL or filename]

[Key points, reactions, relevance to current work]
```

Missing sections are fine. Claude extracts what's there.

---

## Roles

Claude operates in one of 11 roles depending on what you're working on. You never have to declare a role — they activate automatically from the words you use. Responses are prefixed with the active role so you always know which mode is running.

### [EA] Executive Assistant — default

The role Claude starts in every session. Task management, drafting messages, logistics, coordination. Makes reasonable assumptions and flags them. Action over perfection.

**No trigger needed** — this is the baseline.

> *"Send a follow-up to [name] about the Q2 planning doc"*

---

### [PM] Project Manager

Breaks work into phases with owners, dependencies, and acceptance criteria. Lightweight planning that can evolve.

**Triggers:** "plan out", "break down", "help me figure out the work", "what are the milestones"

> *"Break down the migration to the new auth service into milestones"*

---

### [Editor] Editor

Drafts and edits content matching your voice from `context/writing-style.md`. Prioritizes clarity over completeness. For reviews: inline suggestions + summary of the 1-2 biggest changes needed.

**Triggers:** "draft", "write", "review", "proofread", "help me word this"

> *"Draft a message to the team about the on-call rotation changes"*

---

### [DE] Distinguished Engineer

Technical architecture and trade-offs at a peer level. Skips fundamentals, defaults to challenging rather than validating. Surfaces scale, cost, and operational complexity implications.

**Triggers:** "what do you think about [tech decision]", "walk me through the trade-offs", architecture questions

> *"What do you think about moving our session storage to Redis?"*

---

### [Coach] Coach

Prepares you for difficult conversations with specific language. Frames feedback as observable behavior + impact + ask. For 1:1s: surfaces what the person likely needs vs. what's on the agenda.

**Triggers:** "1:1", "how do I approach", "give feedback", "help me prepare for this conversation", "performance"

> *"Help me prepare for a performance conversation with someone who's consistently missing deadlines"*

---

### [Sparring] Sparring Partner

Adversarial by design. Finds problems before they're real. Anticipates pushback from leadership, the team, customers, and your future self. Does not soften criticism.

**Intensity modes:**
- Default: top 3-4 concerns with reasoning
- "really stress test this": gloves off
- "quick gut check": top 2 concerns only

**Triggers:** "poke holes", "stress test", "devil's advocate", "challenge this", "what am I missing"

> *"Poke holes in my plan to merge the platform and infrastructure teams"*

---

### [Founder] Founder Lens

Applies first-principles frameworks from `context/principles.md` to current decisions. Key questions: Is this derived from first principles or copied? Does this require courage? Would someone who genuinely cares do it this way?

**Triggers:** "first principles", "channel the founder", "what would [X] say about this"

> *"Apply first principles thinking to our build vs. buy decision on the billing system"*

---

### [Strategist] Strategist

Multi-quarter thinking, org design, systems and second-order effects. Challenges what you're optimizing for. Flags when tactical decisions are making strategic choices by default.

**Triggers:** "multi-quarter", "org design", "roadmap", "how do we think about the next [period]", "staffing model"

> *"Help me think through the org design for scaling from 20 to 35 engineers"*

---

### [IC] Incident Commander

Active incident mode. Immediate: what do we know, what's the impact, who's working it? Drives to mitigation first, root cause second. Tracks timeline and comms as you go. Closes out with postmortem and follow-up ticket.

**Triggers:** "war room", "we're down", "p0", "production issue", active incidents

> *"We have a P0 — payment processing is down across all regions"*

---

### [Research] Researcher

Gathers before synthesizing. Cites sources, flags confidence levels. Ends with: what this means for us, what we should do differently.

**Triggers:** "deep dive", "find out about", "what does the data say", "research"

> *"Deep dive on how companies our size are structuring platform teams"*

---

### [Interviewer] Interviewer

Generates interview questions mapped to competencies. Synthesizes debrief signal across interviewers, surfaces conflicts, flags gaps. Delivers a hire/no-hire recommendation with rationale.

**Triggers:** "interview prep", "candidate", "debrief", "hiring"

> *"Help me prep interview questions for a Staff Engineer focused on distributed systems"*

---

## Slash commands

### `/morning`

Run at the start of every day. Pulls previous night's EOD notes, checks Jira for overdue tickets and new P1/P2 bugs, checks PagerDuty for overnight incidents, checks Datadog for monitor alerts. Also ingests yesterday's daily note into the wiki if it wasn't already processed, and surfaces active wiki threads relevant to today.

**Reads:** `reports/daily/` (yesterday), Jira, PagerDuty, Datadog, `wiki/daily/` (yesterday), `wiki/hot.md`
**Writes:** `wiki/people/`, `wiki/hot.md`, `wiki/log.md` (if yesterday's note wasn't yet ingested)
**Output:** Structured briefing in the terminal

---

### `/eod`

Run before you close the laptop. First, automatically ingests today's Obsidian Daily Note — updating wiki people pages, filing decisions, extracting action items — so its smart prompts are already informed by your actual meeting notes. Then asks targeted follow-up questions based on what it found in the note, Jira, and PagerDuty. Captures wins to the bragdoc and saves a daily summary.

**Reads:** `wiki/daily/` (today), `wiki/log.md`, PagerDuty, Jira, `decisions/`, `reports/daily/`
**Writes:** `wiki/people/`, `wiki/hot.md`, `wiki/index.md`, `wiki/log.md`, `inbox.md`, `bragdoc/YYYY-MM-DD.md`, `reports/daily/YYYY-MM-DD.md`

---

### `/triage`

Processes everything in `inbox.md`. Categorizes each item as action, reference, or done. Creates Jira tickets for actions (with inferred priority), files reference items to the right `context/` or `decisions/` file, and clears the inbox. Unclear items stay with a `[?]` prefix.

**Reads:** `inbox.md`
**Writes:** Jira tickets, `context/`, `decisions/`, clears `inbox.md`

---

### `/weekly-ops`

Run on Fridays. Queries Jira for bug counts and SLA status by severity across teams, PagerDuty for incidents and MTTR, Datadog for monitor health and SLO status. Cross-references for escalation candidates and patterns. Saves a formatted ops report to `reports/weekly/`.

**Reads:** Jira, PagerDuty, Datadog
**Writes:** `reports/weekly/YYYY-WXX.md`

---

### `/1on1-prep [name]`

Prepare for a 1:1 or key meeting with a specific person. Reads their full wiki page — every prior meeting, open commitments, growth arc, and patterns — then cross-references their recent Jira activity. Generates structured talking points. After the meeting, prompts for a 2-3 sentence summary and logs it back to their wiki page.

If no wiki page exists for this person yet, it creates a stub automatically.

**Reads:** `wiki/hot.md`, `wiki/people/[name].md`, Jira (if direct report)
**Writes:** `wiki/people/[name].md`, `wiki/hot.md`, `wiki/log.md`
**Output:** Follow-up items, what they likely want to discuss, development thread, one thing to listen for

---

## Your daily workflow

### Morning

```
cd ~/Projects/daily-driver
claude
/morning
```

You get a briefing: overnight incidents, Jira queue, active wiki threads, today's focus. Anything on your mind goes directly into `inbox.md` — don't filter it, just capture it.

Before any meeting with a direct report or key stakeholder:

```
/1on1-prep [name]
```

### During the day

In Obsidian, click the Daily Note button (or use the hotkey) to open today's note. Write during or right after each meeting using the templates pre-loaded in the file — a 1:1 block, a strategy meeting block, whatever applies. You don't need to be thorough; even rough notes are useful.

For tasks and ideas that aren't meeting notes, jot them in `inbox.md` as they come up.

When the inbox gets noisy, run `/triage`. It converts action items to Jira tickets and files reference material.

### End of day

```
/eod
```

Claude first reads today's Obsidian Daily Note and compiles it into the wiki — updating person pages, filing decisions, extracting action items to inbox — before asking you anything. Its follow-up questions are already informed by what you wrote: "I see you met with [name] today — anything worth adding beyond the notes?" Answer in plain language. Wins go to the bragdoc. The daily summary gets saved for tomorrow's briefing.

### Friday

```
/weekly-ops
```

Full ops report in ~30 seconds. Bugs by severity, incidents, monitor health, SLAs at risk — formatted and saved.

### The loop

```
Obsidian Daily Note → you write meeting notes during the day
  ↓
/eod → auto-ingests today's note into wiki, then captures wins + actions
  ↓
/morning → ingests yesterday as safety net, surfaces wiki threads + Jira + incidents
  ↓
/1on1-prep → pulls full wiki history before key meetings
  ↓
/triage → inbox becomes Jira tickets
```

The wiki compounds with every session. The bragdoc fills itself. Decisions accumulate. Nothing slips through.

---

## Wiki setup

The wiki uses Obsidian as the browsing layer and Templater for daily note automation. No MCP server required — Claude reads and writes the wiki files directly.

### 1. Open the vault in Obsidian

Obsidian → Manage Vaults → Open folder as vault → select `daily-driver/wiki/`

### 2. Install Templater

Settings → turn off Restricted Mode → Community plugins → Browse → search **Templater** → install → enable

Settings → Templater:
- Template folder location: `_templates`
- Enable **Trigger Templater on new file creation**: on

### 3. Configure Daily Notes

Settings → Core plugins → **Daily notes** → enable

Settings → Daily notes:
- New file location: `daily`
- Template file location: `_templates/daily-note`
- Date format: `YYYY-MM-DD`

### 4. Install optional plugins

Community plugins → install and enable:
- **Dataview** — run queries over page frontmatter, build dynamic dashboards
- **Graph Analysis** — enhanced graph view showing connection strength

### 5. Optional: Obsidian Web Clipper

Install the [Obsidian Web Clipper](https://obsidian.md/clipper) browser extension. It converts web articles to markdown — save directly to `wiki/daily/` and Claude will ingest them on your next `/eod`.

### How it works day-to-day

Each morning (or when your first meeting starts): click the Daily Note icon or use the hotkey. Obsidian creates `wiki/daily/YYYY-MM-DD.md` pre-populated with the five capture templates. Write during or after each meeting. Run `/eod` at the end of the day — it handles everything else automatically.

---

## MCP setup

MCP (Model Context Protocol) is how Claude Code connects to external services. This workspace uses four integrations, all configured in `.mcp.json`.

> `.mcp.json` is gitignored. Your credentials never leave your machine.

### Atlassian (Jira + Confluence)

1. Go to `id.atlassian.com` → Security → API tokens → Create API token
2. Copy your token and your Atlassian org URL (e.g. `yourorg.atlassian.net`)
3. In `.mcp.json`, set:
   ```json
   "ATLASSIAN_URL": "https://yourorg.atlassian.net",
   "ATLASSIAN_USER_EMAIL": "you@yourorg.com",
   "ATLASSIAN_API_TOKEN": "your-token"
   ```

### Datadog

1. Go to Datadog → Organization Settings → API Keys → New Key
2. Go to Organization Settings → Application Keys → New Key
3. In `.mcp.json`, set:
   ```json
   "DD_API_KEY": "your-api-key",
   "DD_APP_KEY": "your-app-key",
   "DD_SITE": "datadoghq.com"
   ```
   (Use `datadoghq.eu` if you're on the EU site)

### PagerDuty

1. Go to PagerDuty → Integrations → API Access Keys → Create New API Key
2. In `.mcp.json`, set:
   ```json
   "PAGERDUTY_API_TOKEN": "your-token"
   ```

---

## Customizing for your role

### Adding or modifying roles

Open `CLAUDE.md` and add a new role section under `## Roles`. Follow the existing format: name, prefix, trigger phrases, behaviors. Keep roles focused — one mode of thinking per role. If you're unsure of the shape, describe the friction you're trying to address to Claude and it'll help you design it.

### Adding slash commands

Create a new `.md` file in `.claude/commands/`. Describe what Claude should do step by step — what to query, what to read, what to write, and how to format the output. Then add it to the slash command index in `CLAUDE.md`.

### Adding context files

Drop any `.md` file into `context/` and reference it in the relevant role in `CLAUDE.md`. Good candidates: org chart, competitor landscape, product principles, team norms, a vendor evaluation, anything you'd want available across conversations.

### Extending the wiki

Add new wiki directories for domains specific to your role. Good candidates: `wiki/orgs/` for org structure tracking, `wiki/vendors/` for vendor relationships, `wiki/initiatives/` for multi-quarter projects. Add any new directory to the file map in `CLAUDE.md` and the ingest rules in `wiki/WIKI.md`.

To ingest a source on demand (article, doc, report): drop it in `wiki/daily/` with a `## Reading:` header, or paste directly into a daily note. `/eod` will pick it up.

To lint the wiki (find orphaned pages, stale open items, missing cross-references): say "lint the wiki" in a Claude session — it reads the index, checks for gaps, and suggests cleanup.

### Start small

You don't need all 11 roles and 5 commands on day one. Start with the `/morning` + `/eod` loop and write a few daily notes. The wiki will start compounding automatically. Add roles and commands as specific friction points emerge.

---

## Adapting for your org

This workspace was built for Jira, Confluence, Datadog, and PagerDuty. If your org uses different tools, swap them out in `.mcp.json` and update the relevant commands and role references in `CLAUDE.md`.

| This workspace uses | Common alternatives |
|---|---|
| Jira | Linear, GitHub Issues, Shortcut |
| Confluence | Notion, Coda |
| Datadog | Grafana, New Relic, Honeycomb |
| PagerDuty | OpsGenie, VictorOps |

Most tools have community MCP servers. If one doesn't exist yet, you can configure a custom MCP server against any REST API.

---

## Migrating to a new machine

Everything committed to git migrates automatically — `CLAUDE.md`, all slash commands, all context files, all reports and bragdoc entries.

The one thing that doesn't live in git is Claude's memory files (`~/.claude/projects/`). To carry those over:

```bash
# On your old machine
cp -r ~/.claude/projects/<project-hash>/memory/ ~/Desktop/memory-backup/

# On the new machine, after cloning and opening the project once
cp -r ~/Desktop/memory-backup/ ~/.claude/projects/<new-project-hash>/memory/
```

The project hash is derived from the directory path, so it'll differ on a new machine. Open Claude Code in the cloned project first to let it create the directory, then copy your memory files in.

Don't forget to re-enter your API credentials in `.mcp.json` — they're gitignored and won't transfer.

---

*Built with Claude Code.*
