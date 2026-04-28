# Daily Driver — Roadmap

Ideas and potential additions. Not commitments — a backlog to pull from when something becomes worth the build cost.

**Rule:** Only add something here if you'd use it more than 3 times. Only build it when the manual version is painful enough to justify encoding.

---

## In progress / next up

*(move items here when actively working on them)*

---

## Potential additions

### Obsidian migration

**What:** Replace the `context/`, `decisions/`, and `bragdoc/` directories with an Obsidian vault. Obsidian is local-first, markdown-native, and supports graph linking between notes — a natural fit for how this workspace already works.

**Why:** Better note-taking, backlinks between decisions and context files, graph view across everything you've written. Already compatible with this repo's file structure.

**What's needed:** A local Obsidian MCP server to give Claude read/write access to the vault. Community options exist; maturity is still developing.

**When to do it:** After settling in at CTCT and validating that the current file structure is working. Don't migrate during onboarding chaos.

---

### Personal to-do tracking

**What:** A `todos.md` file for personal tasks that don't belong in Jira — reminders, development goals, things only you need to track. A `/todo` command to add, complete, and surface items.

**Why:** Not everything is a Jira ticket. The inbox → triage → Jira loop is right for engineering work, but personal commitments need a lighter-weight home.

**Integration with `/morning`:** Surface overdue personal todos alongside the Jira queue.

**Files:** `todos.md`, `.claude/commands/todo.md`

---

### Delivery metrics (DORA)

**What:** A `/dora` command that produces a weekly DORA scorecard — deployment frequency, lead time for changes, change failure rate, and MTTR. Cycle time and throughput from Jira.

**Why:** DORA metrics tell the story of *how* the team is shipping, not just *what* shipped. Essential for a Director-level view of engineering health and for conversations with leadership.

**Integrations needed:**
- CI/CD system (GitHub Actions, Jenkins, etc.) for deployment frequency and lead time
- Jira for cycle time and throughput
- PagerDuty already covers MTTR (in `/weekly-ops`)
- GitHub/GitLab for PR aging

**Output:** Weekly DORA scorecard saved to `reports/weekly/`, surfaced in `/weekly-ops`.

**Files:** `.claude/commands/dora.md`, update `CLAUDE.md` to reference it

---

### User research & product signal

**What:** A `research/` directory for synthesized user interview notes, NPS data, support ticket themes, and usage trends. A `/research-digest` command that synthesizes this material and surfaces product signal relevant to current engineering priorities.

**Why:** Engineering Directors who stay close to customers make better technical decisions. Encoding a research layer connects the engineering work to the customer problem.

**Integrations to consider:**
- Amplitude or Mixpanel for product usage data
- Zendesk or Intercom for support ticket trends
- Manual: paste in synthesized interview notes, NPS data, customer feedback

**New role:** `[Research]` already exists — extend it to be research-data-aware when `research/` files are present.

**Files:** `research/` directory, `.claude/commands/research-digest.md`

---

### 1:1 tracking

**What:** A `1on1s/` directory with a file per direct report. Running notes: what was discussed, commitments made, development goal progress. A `/1on1-prep` command that loads a person's file, checks their recent Jira activity, and generates talking points.

**Why:** Right now coaching conversations are captured loosely in `/eod`. A structured 1:1 layer builds a longitudinal view of each person's growth — invaluable for performance reviews, promotion cases, and coaching continuity.

**Workflow:**
- Before the meeting: `/1on1-prep [name]` → talking points + recent activity
- After the meeting: `/eod` appends summary to their file
- At review time: load their file for a full arc of the relationship

**Files:** `1on1s/` directory, `.claude/commands/1on1-prep.md`, update `/eod` to append to 1:1 files

---

### Hiring pipeline

**What:** A `hiring/` directory with open role specs and candidate tracking. A `/hiring-pipeline` command that gives a snapshot of every open role and where each candidate stands.

**Why:** The [Interviewer] role exists but has no structured data to work with. Hiring is a major Director responsibility — it deserves first-class tracking.

**Files:** `hiring/` directory with one file per open role, `.claude/commands/hiring-pipeline.md`

---

### Business metrics layer

**What:** Once onboarded at CTCT, map out how the company aggregates data from its services and third-party sources. Add a `context/data-architecture.md` describing key data pipelines and metric definitions. Extend `/weekly-ops` to include business health metrics alongside engineering ops.

**Why:** The best engineering decisions are made with business context. A Director who can connect engineering health to business metrics (MAU, deliverability, churn signals, email send volume) has a much stronger voice in strategic conversations.

**What to capture:**
- Internal: how CTCT's services report metrics, where the data lives
- Third-party: market data, competitive benchmarks, industry standards for email deliverability
- Key business KPIs relevant to engineering

**New role to consider:** `[Data]` — knows CTCT's data architecture, can interpret metric movements in context.

**Files:** `context/data-architecture.md`, update `/weekly-ops`

---

### Additional slash commands (smaller scope)

| Command | What it would do | Effort |
|---|---|---|
| `/standup` | Generate async standup from yesterday's Jira activity | Low |
| `/postmortem` | Scaffold a postmortem doc from a PagerDuty incident | Low |
| `/announce` | Draft a team announcement using your writing style | Low |
| `/retro-prep` | Pull sprint data and draft retro prompts for the team | Medium |
| `/okr-check` | Assess progress against current quarter's OKRs | Medium |

---

## Completed

*(move items here when shipped)*

- [x] Initial workspace setup — CLAUDE.md, roles, integrations, file structure
- [x] Core slash commands — `/morning`, `/eod`, `/triage`, `/weekly-ops`
- [x] Context files — team roster, writing style, principles, working-with-me
- [x] Career bragdoc — LinkSquares highlight reel, career-highlights from resume
- [x] README — full documentation for open-source sharing
- [x] GitHub remote — `github.com/da-dumont/daily-driver`
