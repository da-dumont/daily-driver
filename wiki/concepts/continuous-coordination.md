---
type: concept
title: "Continuous Coordination"
created: 2026-04-29
updated: 2026-04-29
tags: [engineering, coordination, async, context, decisions, process]
status: mature
related:
  - "[[AI-Native SDLC]]"
  - "[[Problem Brief]]"
  - "[[Builder Manifesto]]"
  - "[[PR as the Bottleneck]]"
---

# Continuous Coordination

## Core thesis

Coordination is not an event. It's an always-on system.

Most teams operate with context scattered across Slack, docs, meetings, and tickets. Engineers reconstruct intent from partial signals. Alignment lags behind the work. This creates duplicated effort, shallow exploration, inconsistent decisions, and "I didn't know that" failures.

Continuous Coordination replaces batch coordination (planning, standups, grooming) with continuous alignment through written context and visible work.

> Context explicit. Intent visible. Decisions traceable.

---

## The 6 Principles

### 1. Lead with Context
Don't assign tasks. Explain the situation.

- Bad: "Build endpoint for X"
- Better: "Customers are failing to complete onboarding because X is unclear. We think Y is the cause."

Context includes: what is happening, why it matters, constraints, signals/data. Without this, teams can't explore or decide effectively.

### 2. Tell the Future (Intent > Instructions)
Don't just say what to do. Say where things are going.

> "We expect onboarding to move toward self-serve configuration over time."

This allows teams to make better local decisions, avoid rework, and align without constant approval.

### 3. Write Things Down
If it's not written, it doesn't scale. Writing forces clarity, reduces ambiguity, and enables async coordination. Artifacts matter more than meetings.

### 4. Work in the Open
Exploration, thinking, and progress should be visible — not hidden spikes or private experimentation, but shared prototypes, side-by-side comparisons, evolving problem briefs. Enables faster feedback and shared understanding.

### 5. Continuous Updates Over Batch Sync
Replace standups and large planning sessions with small, frequent updates, evolving documents, and visible progress.

> No one needs a meeting to understand what's going on.

### 6. Coordination Happens Through Loops

**Big Loop (Direction)** — goals, strategy, major decisions, risks. Runs weekly.

**Small Loop (Execution)** — day-to-day progress, discoveries, changes in understanding. Runs daily.

Both loops must be visible and updated continuously.

---

## What this enables

- Faster exploration
- Better decisions
- Less thrash
- Higher autonomy
- Fewer meetings

**But only works if:**
- Leaders enforce clarity
- Teams actually write things down
- Decisions are made, not avoided

---

## Mapping to activities

| Activity | Principle |
|---|---|
| Problem Brief | Lead with Context |
| Exploration | Work in the Open |
| Convergence | Tell the Future |
| Async Updates | Continuous Updates |
| Decision Logs | Write Things Down |
| Visible Work | Shared Context |

*See [[AI-Native SDLC]] for how this applies phase by phase. See [[Problem Brief]] for the primary written artifact.*
