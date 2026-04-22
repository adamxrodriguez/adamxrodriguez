# Adam Rodriguez — Senior Software Engineer

I ship production software. React/TypeScript on the front. Node/Next.js and cloud on the back.  
I care about clean systems, fast feedback loops, and work that actually moves the needle.

- **10+ yrs** building enterprise features (healthcare, data, dashboards)
- **React/Next.js, Node, TypeScript, Python**; CI/CD with **GitHub Actions/Jenkins**
- Comfort in the trenches: debugging flaky pipelines, profiling, cost/latency chops

> Some days you don’t feel it.  show up anyway.

---

## Selected Work

- **Metamorphosis (Kafka Observability)** — monitoring  
  Dashboards & tooling that reduce triage time and make message flow visible at a glance.  
  Org repo → https://github.com/oslabs-beta/Metamorphosis

- **Miracle Health (Next.js/TypeScript)** — full-stack features, auth, typed APIs, CI  
  Patterns I like: request validation with Zod, React Query, error boundaries, health checks.  
  Repo → https://github.com/adamxrodriguez/miracle-health

- **Yatch Hub (NextJS/React)** — Yatch dashboard workflow tool  
  Focus on accessibility, keyboard shortcuts, undo/redo, local persistence.  
  Repo → https://github.com/adamxrodriguez/nextjs-dashboard

- **Sofle RGB (keyboard firmware & tooling)** — customization, reproducible builds  
  Notes on low-level configs, ergonomics, and build repeatability.  
  Repo → https://github.com/adamxrodriguez/sofle-rgb-keyboard

---

## How I work

- **Ship small, ship daily.** CI and tests make change cheap and safe.  
- **If it isn’t observable, it isn’t done.** Logs, metrics, traces, healthz.  
- **Pragmatic by default.** Simple > clever. Measure, then optimize.

> I’ve failed more times than I’d admit, but every time I did, I learned something worth keeping.

---

## Toolbox

**Front-end:** React, Next.js, TypeScript, Redux, SWR/React Query, Playwright, Vitest  
**Back-end:** Node, Express/Next API Routes, Python, Kafka, Postgres/Redis  
**DevOps:** GitHub Actions, Jenkins, Docker, OpenAPI  
**Patterns:** rate limiting, idempotency, retries, circuit breakers, feature flags

---

## Case Studies (short reads)

- **Making deployments boring:** wired CI (lint/test/build), added coverage gates, shaved MTTR.  
- **Typed boundaries:** Zod-validated API layer + React Query for cache-aware UX.  
- **Fast feedback:** Playwright smoke tests on PRs; bugs caught before prod.

---

## Contact

- **LinkedIn:** https://www.linkedin.com/in/adamrodriguez  
- **Email:** adamxrodriguez@gmail.com
- **Location:** Florida (EST)

> Don’t wait to feel ready — start.




Development Standards Meeting Notes
April 22, 2026 | ECMS Team

Purpose
Informal discussion to audit existing dev standards — identify gaps, outdated docs, and how to better organize/manage going forward.

Key Discussion Points
Standards Categorization
Tye proposed splitting standards into two distinct tracks:
	•	Coding Standards — enforced at the code level (no warnings/errors, clean code, logging, etc.) — governed by Joe and Tye
	•	Support/Operational Standards — apply to QA, engineers, and ops regardless of role (program grouping, error paths, alerting, purge configs) — governed by Sandy’s team
Identified Gaps
	1.	Program grouping — every deployed program must belong to a program group; not formally documented anywhere
	2.	Error path naming/format — specific format standard exists for alerting purposes, not widely known
	3.	Purge and alert configuration — often missed at project setup; should be considered upfront
	4.	Logging standards — recurring pain point:
	•	No clear consensus on error vs. warning vs. info levels
	•	Error messages should stand alone with enough context (content ID, image ID, what was happening)
	•	Avoid noisy info logs on idle program cycles
	•	Large batch jobs should log progress milestones; coordinate with ops on frequency
	•	Debug/trace log calls should be in place so QA can drop log levels in stage
	5.	Python standards — needed as Python usage is growing; suggestion to standardize linter tooling (Windsurf or similar) as part of feature completion workflow
	6.	Legacy ASP.NET — branching strategy may not apply; needs clarification
	7.	Two separate branching strategy docs — UI (with stage branch, tied to Jenkins) vs. backend; team not universally aware both exist
Documentation & Discovery
	•	Existing standards docs are scattered, inconsistently tagged in Content Central, and not centrally indexed
	•	Suggestions raised:
	•	GitLab repo for standards — enables change alerts/subscriptions (well-received)
	•	AI/admin site documentation tab — centralized hub with links
	•	Better Content Central tagging — fix discoverability at the source
	•	Admin Central dashboard — link standards alongside operational tools
	•	General agreement: a central index or hub is needed, whether it points to Content Central, GitLab, or both

Decisions / Direction
	•	Tye will rename the existing IM group and use it for ongoing standards discussion
	•	Coding standards ownership: Joe + Tye
	•	Support/operational standards ownership: Sandy’s team (with Joe/Tye support)
	•	Logging identified as the first priority gap to address

Action Items



|Item                                                    |Owner                            |
|--------------------------------------------------------|---------------------------------|
|Collect full list of gaps                               |Kourtney (KG) — lead and maintain|
|Review/share notes from today                           |Tye → follow up with Adam        |
|Form small working groups (3 people, cross-functional)  |Tye/KG to organize               |
|First working group focus: **logging standards**        |TBD — 1-2 engineers + 1-2 ops    |
|Evaluate GitLab repo as standards home                  |Team to consider                 |
|Review branching strategy docs for accuracy/completeness|TBD                              |
|Define Python linting/standards approach                |TBD                              |

Next Steps
Working groups will develop solutions independently, then present back to the full team for feedback. KG coordinates scheduling of those sessions.​​​​​​​​​​​​​​​​



