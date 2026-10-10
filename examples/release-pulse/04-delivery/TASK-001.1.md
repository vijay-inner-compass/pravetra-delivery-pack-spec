# TASK-001.1 — Ensure the application complies

- **Component:** Primary Database · sub-task of TASK-001 · **Status:** not_started · **Parallel-safe:** No
- **Depends on:** TASK-001 · **Unlocks:** (none)
- Also follow the common rules in `07-agent/COMMON_RULES.md` (read it once; it applies to every task).

## Outcome
Ensure the application complies with internal data protection.
> **Requirement:** Ensure the application complies with internal data protection policies, including data retention and access controls.

## Done when
- [ ] Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Ensure the application complies with internal data protection policies, including data retention and access controls.
- [ ] Every acceptance criterion listed in Tests has a passing test, and the checkpoint notes name the test that proves it.

## Write these tests first
- positive case: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Ensure the application complies with internal data protection policies, including data retention and access controls.
- negative case: invalid, unauthorised or malformed input for this behaviour is rejected with a clear error.
- Also: Acceptance (positive) for [Must] Ensure the application complies with internal data protec...: Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Ensure the application complies with internal data protection policies, including data retention and access controls.

## Out of scope
- the responsibilities of the other components - API / Backend Service, Data Quality, Release Health Analytics, Digest Worker, Ingest Worker, Scoring Worker, Web Client.

## Applicable decisions
- [2e256e04822c45e682a8e122297a8f72] Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process
- [83bdfa6479364845ba31d373b5805387] Technology: a SQLite-backed job table polled by the hosted background services
- [ce1b21ededfb41c2b326791ecc0ae64b] Technology: ASP.NET Core Web API with polling mechanism
- **Must not contradict** any decision listed above.

## Reviewer checklist
- [ ] Every "Done when" item is met (1 listed), each shown by a named test or check.
- [ ] Every test under "Write these tests first" exists, failed before the change, and passes now.
- [ ] The applicable decisions and the common rules are respected and nothing contradicts them.
- [ ] The out-of-scope items are untouched.
- [ ] No unrelated changes: the diff stays inside the allowed paths and only this sub-task's behaviour changed.

## Prohibited (this task)
- Do not substitute, replace, or alter the locked decision for Technology (C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process).
- Do not substitute, replace, or alter the locked decision for Technology (a SQLite-backed job table polled by the hosted background services).
- Do not substitute, replace, or alter the locked decision for Technology (ASP.NET Core Web API with polling mechanism).

## Target Scope
| Path | Status | Note |
| --- | --- | --- |
| `(proposed) primarydatabase/` | Proposed | No baseline exists for this path — treat it as a starting suggestion, not a fixed location. |

**Allowed changes:** Add, modify, or remove files within this task's target scope (primarydatabase/) that this requirement needs. Add unit and integration tests under tests/ for this requirement of 'Primary Database'. Update service registration in the composition root / dependency injection module where the behaviour needs it.

## Implementation Steps
1. Confirm the skeleton from TASK-001 builds and its health check passes.
2. Implement: Ensure the application complies with internal data protection policies, including data retention and access controls.
3. Follow the component's recorded responsibilities (see Current State Evidence) wherever they apply to this behaviour.
4. Align the component interface with its contract: (see Contract)
5. Keep to the component's data design: Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own). Data lifecycle and residency policy: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….

## Contract
Database access through the chosen data-access layer with connection pooling, command timeouts, and retry-on-failure strategies.

## Quality and Security (this task)
- Data handling and retention specification: Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own). Data lifecycle and residency policy: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….
- Architecture decomposition boundary: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.
- Non-functional target (Ensure the application is available during working hours,...): Ensure the application is available during working hours, with monitoring in place to detect and alert on any downtime.
- Non-functional target (Process incoming webhook events with a latency of no more...): Process incoming webhook events with a latency of no more than 2 seconds for 95% of events, ensuring timely updates to release health scores.
- Non-functional target (Implement data encryption in transit and at rest to prote...): Implement data encryption in transit and at rest to protect sensitive incident data, ensuring compliance with internal security policies.
- Non-functional target (Maintain an audit log of all actions taken within the app...): Maintain an audit log of all actions taken within the application, including data ingestion, scoring calculations, and user access, retaining logs for a minimum of 24 months.
- Non-functional target (Ensure the application is scalable to handle increased da...): Ensure the application is scalable to handle increased data volumes as the number of deploys and incidents grows, with a target of supporting at least 1000 events per hour.
- Non-functional target (Ensure the application complies with internal data protec...): Ensure the application complies with internal data protection policies, including data retention and access controls.
- Non-functional target (Ensure the application is maintainable, allowing for upda...): Ensure the application is maintainable, allowing for updates and modifications without significant downtime or disruption to service.

## Current State Evidence
Builds on the skeleton of 'Primary Database' delivered by TASK-001. Greenfield component per Solution Blueprint. Target responsibilities:
• Provide durable, ACID-compliant persistence for all domain entities and audit events.
• Enforce relational integrity, foreign key constraints, and unique indexes.
• Support point-in-time recovery and snapshot durability.
- **Source references:** BlueprintComponent: Primary Database (`fb295674ebc14ea29a0f9352f6066749`); Requirement: [Must] Ensure the application complies (`f4dc4a536bc7489098645b6bfaf808ce`); TechnologyDecision: Technology: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (`2e256e04822c45e682a8e122297a8f72`); TechnologyDecision: Technology: a SQLite-backed job table polled by the hosted background services (`83bdfa6479364845ba31d373b5805387`)
- **Baseline:** No existing-system baseline — greenfield project. Every target path below is Proposed, not discovered.

## Commands
| Label | Command |
| --- | --- |
| Build (dotnet) | `dotnet build --nologo` |
| Test (dotnet) | `dotnet test --nologo` |

**Checkpoint:** when done, update `07-agent/execution-state.json` (fields: tasks[].status, tasks[].completedAt, nextSafeAction) as the common rules describe.
