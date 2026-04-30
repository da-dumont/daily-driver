---
type: concept
title: "AI-Native SDLC"
created: 2026-04-29
updated: 2026-04-29
tags: [engineering, AI, process, SDLC, delivery, exploration]
status: mature
related:
  - "[[Continuous Coordination]]"
  - "[[Problem Brief]]"
  - "[[Builder Manifesto]]"
  - "[[PR as the Bottleneck]]"
---

# AI-Native SDLC

## Core thesis

Work no longer follows: `plan → build → review → ship`

The new loop is:

> **clarity → exploration → convergence → commit → validate → ship**

The old model was organized around writing code as the bottleneck. Code is now cheap. The bottleneck is understanding the problem, deciding what should exist, and validating it's correct. Wrong decisions are expensive.

---

## The Six Phases

### 1. Clarity — Problem Framing
**Goal:** Shared understanding of the problem before any building starts.
**Output:** [[Problem Brief]]

A Problem Brief answers: what is happening, why it matters, what the evidence is, what we hypothesize, and what success looks like. No exploration starts without one.

### 2. Exploration
**Goal:** Generate multiple viable approaches fast.

- Parallel, AI-assisted prototyping
- 2–3 competing options with real outputs
- Shared openly — not hidden spikes

**Output:** Competing options with prototypes, screenshots, and explicit tradeoffs.

Example:
- Option A: simplified UI flow
- Option B: AI-assisted suggestion
- Option C: guided wizard

### 3. Convergence
**Goal:** Decide what is correct. Make tradeoffs explicit.

Mechanism: async doc or short focused meeting — not a committee.

**Output:**
```
## Decision
[What we chose]

## Why
[Reasoning]

## Tradeoffs
[What we're giving up]

## Risks
[What could go wrong]
```

### 4. Commit — Execution
**Goal:** Implement with minimal ambiguity.

Tickets at this phase are concrete:
- "Implement segment suggestion service" ✓
- "Explore segmentation improvements" ✗

**Output:** Small, clear tickets in Jira/Linear that map to the convergence decision.

### 5. Validation
**Goal:** Ensure correctness — that the implementation matches intent and is technically sound.

Mechanisms: PR review, CI/CD, testing, observability.

PRs at this phase should answer:
- Does this match the decision?
- Is it correct?
- Are edge cases handled?

Not: "What is this doing?" *(See [[PR as the Bottleneck]])*

### 6. Ship
Release to real users. Measure specific signals, not vague engagement. Design for learning — expose early to cohorts, define kill criteria upfront. *(See [[Builder Manifesto]] — Principle 15)*

---

## Tactical Playbook (Constant Contact)

### Exploration phase in practice
- 2–3 approaches created, AI-assisted prototyping
- Outputs shared openly (prototypes, tradeoffs)
- No convergence until options are real, not theoretical

### Continuous async updates
Updates replace standups. They live in the same doc or thread and evolve over time:

```
Update: Exploration — Option B performing best in internal testing. Model accuracy ~82%.
Update: Risk — Edge cases failing for large lists.
Update: Decision — Moving forward with Option B.
```

### Double Loop in practice

**Big Loop (Weekly)**
- What problems matter
- What decisions were made
- What risks exist

**Small Loop (Daily)**
- What changed
- What was learned
- What direction is shifting

---

## What this is not

This is not less structure. It's different structure:
- Earlier in the lifecycle
- Focused on decisions
- Built around context instead of tasks

Done well: teams move faster, decisions improve, noise decreases.
Done poorly: chaos increases quickly.

The difference is discipline around clarity, visibility, and decision-making.

*See [[Continuous Coordination]] for the coordination system that makes this work. See [[Problem Brief]] for the primary artifact.*
