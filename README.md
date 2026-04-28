# Daily Driver

A persistent Claude Code workspace for engineering leaders. Not a one-off AI session — an operating environment that accumulates context, connects to your tools, and gets better the more you use it.

Built for a Director of Engineering at Constant Contact, but adaptable to any engineering leadership role.

---

## What this is

Most AI interactions start cold. You open a session, do a thing, close it, and all context disappears.

A daily driver is different. It's a workspace with memory (via files), opinions (via encoded roles), and live data (via integrations). You open Claude Code here in the morning and drive your entire day from it — briefings, task management, drafting, decision support, incident response, and more.

The core insight: when you connect your tools, encode how you think, and let context accumulate over time, the whole becomes greater than the sum of its parts. Information has a lifecycle. Things don't fall through the cracks. Invisible work gets captured. The cognitive load of remembering, tracking, and connecting gets offloaded to something that's more consistent at it than you are.

---

## Prerequisites

- [Claude Code](https://claude.ai/code) installed and authenticated
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

1. Fill in `.mcp.json` with your credentials (see [MCP Setup](#mcp-setup))
2. Update `context/team-roster.md` with your team structure
3. Update `context/writing-style.md` with your voice preferences
4. Update `context/principles.md` with leadership frameworks you want to apply
5. Open Claude Code: `claude` in the project directory

That's it. Claude reads `CLAUDE.md` on every session and orients itself.

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
└── .claude/
    └── commands/               # Slash command definitions
        ├── morning.md
        ├── eod.md
        ├── triage.md
        └── weekly-ops.md
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

Run at the start of every day. Pulls previous night's EOD notes, checks Jira for overdue tickets and new P1/P2 bugs, checks PagerDuty for overnight incidents, checks Datadog for monitor alerts, and applies a day-of-week focus nudge from `CLAUDE.md`.

**Reads:** `reports/daily/` (yesterday), Jira, PagerDuty, Datadog
**Output:** Structured briefing in the terminal

---

### `/eod`

Run before you close the laptop. Silently gathers context first (what incidents happened today, what Jira tickets closed, what decisions were logged), then asks smart follow-up questions based on what it found. Captures your brain dump as action items in `inbox.md` and wins in the bragdoc. Saves a daily summary to `reports/daily/`.

**Reads:** PagerDuty, Jira, `decisions/`, `reports/daily/` (today's morning)
**Writes:** `inbox.md`, `bragdoc/YYYY-MM-DD.md`, `reports/daily/YYYY-MM-DD.md`

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

## Your daily workflow

### Morning

```
cd ~/Projects/daily-driver
claude
/morning
```

You get a briefing: overnight incidents, Jira queue, today's focus. Anything on your mind goes directly into `inbox.md` — don't filter it, just capture it.

### During the day

Work naturally. Use trigger phrases to shift into the role you need without declaring it. Jot thoughts, tasks, and ideas into `inbox.md` as they come up.

When the inbox gets noisy, run `/triage`. It converts action items to Jira tickets and files reference material — you don't have to think about where things go.

### End of day

```
/eod
```

Claude asks smart questions based on what actually happened — not a generic template. It knows if there was an incident, what you closed in Jira, what decisions you logged. Answer in plain language. It captures wins to the bragdoc and saves a daily summary that tomorrow's `/morning` will surface.

### Friday

```
/weekly-ops
```

Full ops report in ~30 seconds. Bugs by severity, incidents, monitor health, SLAs at risk — formatted and saved. Use it to write your weekly R&D update or share it directly.

### The loop

```
/morning → surfaces yesterday's open loops
  ↓
Work the day → inbox captures what comes up
  ↓
/triage → inbox becomes Jira tickets
  ↓
/eod → captures wins and saves daily summary
  ↓
/morning → surfaces tonight's notes tomorrow
```

The bragdoc fills itself as a side effect. Decisions accumulate in `decisions/`. Nothing slips through.

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

### Start small

You don't need all 11 roles and 4 commands on day one. Start with 1-2 roles that address your biggest friction points and the `/morning` + `/eod` loop. Add more as new patterns emerge. The overhead of maintaining something you don't use will outweigh any benefit from having it.

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
