---
type: concept
title: "Problem Brief"
created: 2026-04-29
updated: 2026-04-29
tags: [engineering, artifact, clarity, process, AI-native]
status: mature
related:
  - "[[AI-Native SDLC]]"
  - "[[Continuous Coordination]]"
---

# Problem Brief

## What it is

The Problem Brief is the primary artifact of the Clarity phase in the [[AI-Native SDLC]]. It creates shared understanding of the problem before any building starts.

It replaces: vague tickets, "build X" assignments, and implicit context passed through meetings.

> No exploration starts without a Problem Brief.

---

## Template

```md
## Problem
What is happening?

## Why it matters
Customer / business impact

## Evidence
Screenshots, logs, metrics, support ticket patterns

## Hypothesis
What we think is causing this

## Success Criteria
What would measurably improve if this were solved
```

---

## Example

```md
## Problem
Users drop off during campaign creation when selecting audience segments.

## Why it matters
Impacts campaign completion rate and revenue.

## Evidence
40% drop-off at segment step. Support tickets cite confusion with segment UI.

## Hypothesis
Segment UI is too complex and unclear for non-technical users.

## Success Criteria
Increase campaign completion rate from 60% → 75%
```

---

## Why it matters

Without a Problem Brief:
- Engineers build solutions to the wrong problem
- Exploration is shallow — teams converge too early on one approach
- Decisions are implicit and untraceable
- Alignment requires meetings instead of reading

With a Problem Brief:
- Context is explicit before work starts (see [[Continuous Coordination]] — Principle 1)
- Exploration is focused on a defined problem space
- Success criteria create a natural kill condition for weak options

---

## When to write one

- Any meaningful feature or change
- Before any exploration or prototyping begins
- When a bug has unclear root cause or scope
- When multiple approaches are plausible

Not required for: dependency bumps, copy fixes, clearly-scoped small changes.
