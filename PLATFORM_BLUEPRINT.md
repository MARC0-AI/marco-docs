# MARCO Platform Blueprint

## Architecture

```text
User
 ├─ MARCO Desktop ── local model, memory, selected files, voice
 │       │
 │       └─ approved capability request ──┐
 │                                        ▼
 └─ MARCO Control Room ── queue, planner, worker, approvals, evidence
                                          │
                                          ▼
                                  GitHub / calendar / connected services
                                  (scoped credentials + human approval)
```

## Shared contracts to build next

### Capability manifest

Every action has a stable identifier, risk class, input schema, output schema,
and audit event. Examples: `task.capture`, `calendar.create`, `file.read`,
`github.create_branch`. The desktop may execute local low-risk capabilities;
the control room governs connected or consequential capabilities.

### Event schema

All systems emit append-only events with `eventId`, `timestamp`, `actor`,
`capability`, `requestId`, `status`, and redacted evidence. Events make the
control room truthful, help recovery, and enable evaluations.

### Approval policy

| Class | Examples | Default |
| --- | --- | --- |
| Local read | Search local memory, list selected files | Allowed |
| Local write | Create a task or local event | Allowed when explicitly requested |
| External read | Read a connected GitHub repository | Allowed after connection |
| External write | Open PR, create calendar event, send message | Confirm before execution |
| Consequential | Merge, deploy, change permissions, spend money | Explicit human approval with audit evidence |

## Reliability bar

- Idempotency keys for external jobs and retries.
- A lease-owning worker with heartbeats and deterministic stale-job recovery.
- Per-capability timeouts, cancellation, and bounded retry policies.
- Test fixtures for provider outages, invalid permissions, and interrupted jobs.
- Evidence links for every completed remote action.
- Metrics for queue latency, worker health, approval time, failure rate, and
  evaluation pass rate.

## Product quality bar

- One identity, vocabulary, and capability name across every interface.
- No false “working” indicators: every status is backed by current evidence.
- A plain-language explanation before a user grants a new permission.
- Full local-only usefulness before a user connects any cloud account.
