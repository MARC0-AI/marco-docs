# MARCO Operating System

## Mission

MARCO is a trustworthy AI operating system for ambitious work: a local-first
assistant for an individual, paired with a permissioned control room for
complex engineering workflows. It should be helpful without inventing work,
safe without being cumbersome, and progressively more capable as users grant
clear permission.

## One product, four surfaces

| Surface | Role | Source of truth |
| --- | --- | --- |
| GitHub (`MARC0-AI`) | Version history, issues, review, release evidence | Merged pull requests and this repository |
| Mac workspace | Local development and desktop runtime | Checked-out repositories plus local tests |
| Replit MARCO Control Room | Web operations interface, queues, approvals, reporting | Verified database/worker state; never simulated activity |
| Codex | Coordinator, implementer, verifier, and documentation steward | This operating system plus test and review evidence |

## Active repositories

| Repository | Responsibility | Current direction |
| --- | --- | --- |
| `marco-core` | Model-agnostic assistant session, tools, and memory orchestration | Local model tools and stable contracts |
| `marco-memory` | Local-only memory persistence and retrieval | Transparent, replaceable storage |
| `marco-desktop` | Private desktop assistant | Chat, tasks, local calendar, selected files, voice, links |
| Replit MARCO Control Room | Permissioned multi-workstream operations dashboard | Queues, approvals, worker health, evidence-based reporting |
| `marco-docs` | Product and system source of truth | This document and the platform blueprint |

## Operating rules

1. There is one product name: **MARCO**. Retire temporary or unrelated names
   from user-facing surfaces.
2. A feature is not complete until it has an owner, a documented boundary,
   verification evidence, and an updated status here.
3. Local actions stay local by default. Files require user selection; browser
   actions require an explicit request; external accounts require connection
   and clear approval.
4. The Replit control room reports actual queue, worker, and approval state.
   It must not display synthetic activity as real work.
5. GitHub changes flow through branches and review. Remote merges, deployments,
   and consequential account actions remain approval-gated.
6. The desktop assistant and control room share concepts and capability names,
   but not privileged credentials or uncontrolled execution paths.

## Current capability state

| Capability | Desktop | Control Room | Status |
| --- | --- | --- | --- |
| Local model chat | Ollama `llama3.2` | Provider key required for LLM planning | Desktop verified |
| Task capture | Local persistent inbox | Durable job queue | Both implemented independently |
| Calendar | Local event store | Not connected to a provider | Local MVP only |
| Files | Explicit per-session selection | Repository evidence and logs | Permission boundaries defined |
| Browser | Explicit URL opening | GitHub adapter design | No unattended automation |
| Voice | Speech output; input when runtime supports it | Not applicable | Desktop MVP |
| GitHub workflow | Local repositories | Approval-gated adapter | Live authenticated actions pending |

## Delivery sequence

1. **Foundation — current:** align product identity, architecture, and local
   assistant/control-room boundaries.
2. **Reliability:** connect the Replit worker to a configured LLM provider,
   repair planner lease and cancellation behaviour, and prove real worker
   lifecycle through tests and evidence.
3. **Unification:** introduce a shared capability manifest and event schema so
   desktop requests can enter the control room only through approved jobs.
4. **Integrations:** add Google/Apple calendar and authenticated GitHub only
   after explicit account connection, scopes, audit logs, and approval UI.
5. **Excellence:** evaluation suites, permissions review, observability, and
   release automation with measurable reliability targets.

## Decision log

| Date | Decision | Why |
| --- | --- | --- |
| 2026-10-21 | Product identity is MARCO | A single name removes fragmented product perception |
| 2026-10-21 | GitHub documentation is the durable product source of truth | It is versioned, reviewable, portable, and available to every build surface |
| 2026-10-21 | Desktop remains local-first; Replit is the permissioned operations plane | Preserves privacy while enabling robust team-scale work |
