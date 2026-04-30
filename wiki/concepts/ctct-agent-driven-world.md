---
type: concept
title: "Constant Contact in an Agent-Driven World"
created: 2026-04-29
updated: 2026-04-29
tags: [strategy, AI, agents, product, infrastructure, CTCT]
status: mature
related:
  - "[[Builder Manifesto]]"
  - "[[AI-Native SDLC]]"
---

# Constant Contact in an Agent-Driven World

## What's changing

Users are no longer the primary interface to software. Agents are.

Instead of logging into tools and building campaigns step by step, users describe outcomes. Agents decide how to get there, pulling in multiple systems along the way.

That means Constant Contact is no longer the place where work starts. It becomes the place where work gets executed.

---

## The shift in position

| | Old model | New model |
|---|---|---|
| **What CC is** | The product | Infrastructure |
| **Value driver** | UI, features, workflows | Agents orchestrate, CC executes |

If we stay anchored to the old model, we get commoditized.
If we lean into the new model, we become critical infrastructure.

---

## What we need to be great at

### 1. Programmatic, composable actions
Agents don't want workflows. They want building blocks.

Expose small, reliable primitives that can be composed:
- `create_draft`
- `generate_segment`
- `apply_template`
- `schedule_send`
- `fetch_performance`

Not one big "create campaign" endpoint. Small steps that compose.

### 2. Deterministic execution
Agents decide what to do. We guarantee it happens correctly.

This is the trust layer:
- Correct audience targeting
- Deliverability
- Compliance
- Auditability

### 3. Clean, accessible data
Agents need context to make decisions. We should expose:
- Contact and segment data
- Engagement history
- Campaign performance
- Metadata around content and timing

If the data is messy or hard to query, agents won't rely on us.

### 4. Agent-friendly interfaces
Not just APIs for developers — interfaces designed for agents:
- Structured inputs and outputs
- Predictable schemas
- Clear tool affordances
- Simulation before execution

The UI becomes secondary. This becomes primary.

### 5. Interoperability across systems
We are one node in a larger system. Agents will pull from CRM, ecommerce, support systems, analytics platforms. We need to accept context, act on it, and return results cleanly.

This is not "integrations" in the old sense. It's participation in a graph.

### 6. Feedback loops
Agents improve based on results. We should expose:
- Open rates, conversions, segment performance, A/B outcomes

So agents can learn and optimize over time.

---

## Required systems

### System layer *(likely exists — needs cleanup)*
- Contact + segmentation service
- Campaign + template service
- Delivery infrastructure (email send pipeline)
- Compliance + policy engine
- Analytics + performance tracking

### Control plane *(the missing piece for most teams)*
- Tool registry (agent-callable actions)
- Context assembly layer (pulls CRM, analytics, CC data together)
- Orchestration engine (plans + executes multi-step workflows)
- Simulation + validation service
- Audit + decision logging

### Data layer
- Unified engagement store (events: open, click, convert)
- Queryable segmentation engine
- Historical campaign performance store
- Feature extraction layer (for "what works" insights)

### Interfaces
- REST APIs (deterministic execution)
- Tool schemas (agent-facing)
- Webhooks / event streams (feedback loops)

---

## How we make money

We move from seats and features to usage and execution:
- Charge per send, segment computation, and action
- Charge for reliable delivery and compliance
- Charge for throughput and priority execution
- Layer in outcome-based pricing over time

We get paid when agents use us to do real work.

---

## Where commoditization happens

If we only provide basic sending, generic segmentation, and interchangeable APIs — agents can swap us out.

## How we avoid it

Focus on what is hard to replace:
- **Deliverability and sender reputation**
- **Compliance and correctness**
- **Clean data and performance insights**
- **Fast, reliable execution**

We become the default system agents trust when email is the action.

---

## Use cases

### Use Case 1: Re-engage dormant customers

**User intent:** "Generate and send a campaign to my dormant users using messaging similar to what performed best last quarter."

**High-level flow:**
1. Agent gathers context (CRM + analytics + CC data)
2. Agent defines dormant segment
3. Agent generates campaign draft
4. Agent simulates performance
5. Agent executes send
6. Agent collects results and learns

**Tool calls + execution:**

```json
// 1. Create dormant segment
POST /segments/create
{
  "rules": [
    { "event": "email_open", "last_seen": ">90d" },
    { "event": "email_click", "last_seen": ">120d" }
  ]
}

// 2. Generate campaign draft
POST /drafts/create
{
  "template_id": "reengagement_v2",
  "inputs": {
    "tone": "friendly",
    "offer": "10% discount"
  }
}

// 3. Simulate before sending
POST /campaigns/simulate
{
  "segment_id": "seg_123",
  "draft_id": "draft_456"
}

// 4. Execute send
POST /campaigns/send
{
  "segment_id": "seg_123",
  "draft_id": "draft_456",
  "schedule": "2026-05-01T10:00:00Z"
}

// 5. Collect results
GET /campaigns/cmp_789/performance
```

**What Constant Contact owns in this flow:**
- Segmentation engine
- Campaign draft surface (optional but strategic)
- Simulation + validation
- Delivery infrastructure
- Compliance + audit
- Performance tracking

**What the agent owns:**
- Orchestration across systems
- Decision-making
- Optimization over time
- Tool composition

---

## The mental model

We are not building a better email marketing tool.

We are building:
> A reliable, trusted execution layer for customer communication that agents can use safely and effectively.
