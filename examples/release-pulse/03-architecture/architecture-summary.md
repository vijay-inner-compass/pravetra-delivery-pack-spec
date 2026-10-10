# Architecture Summary

| Field | Value |
| --- | --- |
| Architecture style | Modular Monolith with Selected Extracted Services |
| Decomposition | Hybrid |
| Branching strategy | GitHub Flow |

Rationale: Most functionality stays in one deployable unit; only the boundaries with a distinct scaling/ownership need are extracted.

## Selected Technology

- **Technology**: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process (rejected alternatives, do not use: Python workers beside a .NET API (a second runtime to build, deploy and monitor); Three separate .NET worker processes (three deployments for one small team group)). Rationale: Server language, framework and hosting model. The owner mandates .NET. One process keeps deployment to a single published build, and hosted services give the workers a lifetime tied to the API host without a second runtime.
- **Technology**: a SQLite-backed job table polled by the hosted background services (rejected alternatives, do not use: an in-process channel (System.Threading.Channels) inside the API host (events queued in memory are lost when the host restarts); a spool folder of JSON files read by the workers (no transactions; a crash can lose or double-process an event)). Rationale: Database and background-work queue. SQLite is the mandated database. A job table written in the same transaction as the event makes the at-least-once, scored-once requirement testable, with no broker to run. Write-ahead mode lets the API read while a worker writes.
- **Technology**: ASP.NET Core Web API with polling mechanism (rejected alternatives, do not use: ASP.NET Core Web API with SignalR). Rationale: The choice between SignalR and polling hinges on the need for real-time updates versus simplicity. SignalR offers a more responsive user experience, which aligns with the requirement for timely insights, but comes with added complexity. Polling is easier to implement but may not meet the latency requirements effectively.

## Component Catalog

| Component | Kind | Responsibilities |
| --- | --- | --- |
| Digest Worker | BackgroundWorker | • Run the digest worker as its own background process, separate from the API service and the other workers. • Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting. • Retry failed items with backoff and record failures in structured logs. |
| Ingest Worker | BackgroundWorker | • Run the ingest worker as its own background process, separate from the API service and the other workers. • Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting. • Retry failed items with backoff and record failures in structured logs. |
| Scoring Worker | BackgroundWorker | • Run the scoring worker as its own background process, separate from the API service and the other workers. • Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting. • Retry failed items with backoff and record failures in structured logs. |
| Web Client | ClientApp | • Provide responsive and accessible user interface for solution workflows. • Coordinate client-side state management, route transitions, and input validation. • Manage authentication sessions and handle operational error display. |
| Primary Database | DataStore | • Provide durable, ACID-compliant persistence for all domain entities and audit events. • Enforce relational integrity, foreign key constraints, and unique indexes. • Support point-in-time recovery and snapshot durability. |
| API / Backend Service | DeployableUnit | • Expose secure RESTful API endpoints for client and external consumers. • Enforce authentication, role-based authorization, and rate limiting. • Coordinate transactional unit-of-work across domain modules. • Emit structured audit logs and operational telemetry. |
| Data Quality | LogicalModule | • Implement core domain logic and invariant validation for: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.; Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.; Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Release Health Analytics | LogicalModule | • Implement core domain logic and invariant validation for: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.; Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.; Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |

