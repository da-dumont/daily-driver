---
type: concept
title: "PR as the Bottleneck"
created: 2026-04-29
updated: 2026-04-29
tags: [engineering, delivery, CI, review, velocity, automation]
status: mature
related:
  - "[[Builder Manifesto]]"
---

# PR as the Bottleneck

## Core thesis

AI sped up how fast we write code. It didn't speed up how fast humans review it. So PR queues become the new constraint.

Most teams try to fix that by adding reviewers. That doesn't scale.

**The shift: make review less necessary.**

> Correctness becomes a system property.
> Review becomes a judgment layer.

---

## The Operating Model

### Phase 1: Reduce Review Load

Make PRs smaller and easier to reason about.

- **Enforce smaller units of change** — soft limit ~300–500 lines; break "build feature X" into API → service → UI → wiring
- **Use stacked PRs** instead of long-lived branches — incremental changes merged continuously
- **Risk-based review:**
  - UI copy change → auto-merge
  - New endpoint → 1 reviewer
  - Auth/permissions → deeper review, 2 approvals
- **AI PR summaries** — reviewer reads intent before diff
  - Example: "Moves contract parsing into async worker. Risk: queue handling + retry logic. No changes to external API."

---

### Phase 2: Shift Validation Left

Move correctness out of human review and into the system.

- **CI is the primary quality gate** — tests, types, linting, contract/schema validation must pass before a human sees the PR
  - API change without schema update → blocked automatically
  - Missing test coverage → blocked
- **Domain-specific guardrails:**
  - Permissions change → verify access matrix tests
  - Analytics pipeline → validate dbt models compile + sample queries run
  - LLM output → enforce schema validation + fallback behavior
- **AI-assisted first pass** — flags missing edge cases, suggests test coverage, highlights risky diffs; removes noise before human review

---

### Phase 3: Redefine the PR

PRs are for judgment, not correctness.

- Reviewer asks: "Does this change make sense?" not "Is this code correct?"
  - "Should this logic live in this service?" ✓
  - "Did you miss a null check?" ✗
- **Auto-merge low-risk changes:** dependency bumps, UI tweaks, small refactors with full coverage
- **Move toward continuous change** — 5–10 small PRs/day, many auto-merged, vs. 1 large PR every 3 days

---

### Phase 4: Fix CI/CD as a System

If CI is slow or flaky, everything collapses.

- **Parallelize aggressively** — split test suites, run jobs concurrently (example: 20 min → 5 min)
- **Run only what changed** — frontend change → skip backend tests; service A change → skip unrelated services
- **Cache everything** — dependencies, builds, test artifacts
- **Eliminate flakiness** — treat like production incidents; flaky CI destroys trust → engineers fall back to manual review → bottleneck worsens

---

## End State

When it's working:
- Most low-risk changes merge automatically
- PRs are small, fast, and focused
- CI enforces correctness
- AI removes repetitive review work
- Humans focus on intent, architecture, and system design

**Continuous validation** instead of batch review.
**Automated enforcement** instead of manual policing.
**Human judgment applied where it matters.**

---

## The Principle

Don't scale review by adding reviewers. Scale by changing what requires review.

*See also: [[Builder Manifesto]] — principles 9 (Review Is the New Bottleneck) and 12 (Reduce the Need for Review)*
