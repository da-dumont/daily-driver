# Dan Dumont — User Profile

This file is the canonical personal profile for the user. Claude reads this at session start to calibrate tone, depth, and collaboration style. It is the in-repo equivalent of persistent memory.

---

## Identity

**Dan Dumont** — Director of Engineering at Constant Contact (started April 2026). Lives in Merrimac, MA. This is a return to CTCT — previously held SEM and EM roles there (Oct 2018–Nov 2021).

Prior role: Director of Engineering at LinkSquares (Jul 2023–Mar 2026), Sr. Engineering Manager before that (Nov 2021). 17+ years in SaaS.

Personal: wife Rachel, three kids (Brooks, Cal, Miller), two red Labs (Yeti and Grizzly). Enjoys travel, lake house, reading, music (eclectic: Avicii to Black Sabbath), sports, staying active, tinkering with AI.

Predictive Index profile: **Maverick** — direct, decisive, results-driven, strong on relationships.

---

## Technical Depth

- Front-end roots: JavaScript, CSS, HTML, React. Has since expanded to full-stack, platform, AI systems, cloud infra.
- Built production agentic AI system on AWS Bedrock (contract extraction, retrieval, workflow automation, natural language interface)
- API & platform strategy across 25+ microservices
- Integrations: Salesforce, Slack, Google Docs, Microsoft Word, Box, SharePoint, Google Drive
- React design systems, NX monorepo, real-time notification systems
- CapEx planning, AWS cost management, vendor negotiations

---

## Leadership Track Record

- 4 teams, 3 EMs, ~20 engineers at LinkSquares (most recent)
- Grew eng throughput ~30% via AI-assisted SDLC without adding headcount
- Onboarded 30+ engineers, cut time-to-first-PR from 2 weeks to <1 week
- Built full career framework (IC + manager track) for 50+ engineers
- Incident response and postmortem practices across eng, support, sales, CS

---

## How Dan Operates

- Works at the product/platform/business intersection — sequences investment, translates eng capacity to commercial outcomes, stays close to the customer problem
- Prefers action over perfection; flags assumptions rather than stalling
- Direct communicator — skip the preamble, get to the point
- Thinks in systems and second-order effects; will push back on tactics that make strategic choices by default
- Defaults to shipping small and learning fast rather than big-bang design

---

## Collaboration Preferences

- Terse responses preferred — no trailing summaries, no restating what was just done
- Treat this workspace as a peer environment — engage at staff/principal level, not tutorial level
- Flag assumptions explicitly rather than asking clarifying questions for every detail
- Commit to the repo often; keep the wiki current

---

## Workspace Setup Notes

On a new machine, after `git pull`:
1. Claude has full context via `CLAUDE.md`, `wiki/`, and this file — no further orientation needed
2. MCP integrations (Jira, Confluence, Datadog, PagerDuty) require API keys configured in `.env` — see `.mcp.json` for the expected variables
3. `.claude/settings.local.json` contains pre-approved permissions — no need to re-approve common git/web operations
