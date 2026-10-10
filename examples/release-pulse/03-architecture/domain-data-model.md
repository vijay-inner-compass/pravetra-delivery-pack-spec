# Domain Data Model & Entity Dictionary

This document specifies the **Domain Data Model, Entity Boundaries, and Schema Requirements** for **E02-release-pulse**. It provides the persistence models, aggregate roots, relationships, and data governance rules required for autonomous coding agents implementing **TASK-001 (Primary Database / Persistence)** and component domain services across **Domain-Driven Design (DDD)**, **Scrum Data Modeling**, **SAFe Architecture Enablers**, and **Enterprise Database Engineering**.

## 1. Architecture & Persistence Context

| Architecture Attribute | Specification |
| --- | --- |
| Architecture Style | Modular Monolith with Selected Extracted Services |
| Decomposition Structure | Hybrid |
| Target Schema Version | v3 |

### Decided Persistence Stack

- **Technology**: a SQLite-backed job table polled by the hosted background services (rejected alternatives, do not use: an in-process channel (System.Threading.Channels) inside the API host (events queued in memory are lost when the host restarts); a spool folder of JSON files read by the workers (no transactions; a crash can lose or double-process an event)). Rationale: Database and background-work queue. SQLite is the mandated database. A job table written in the same transaction as the event makes the at-least-once, scored-once requirement testable, with no broker to run. Write-ahead mode lets the API read while a worker writes.

## 2. Component Entity & Schema Specifications

| Component | Kind | Responsibilities | Data Design & Entities |
| --- | --- | --- | --- |
| Digest Worker | BackgroundWorker | • Run the digest worker as its own background process, separate from the API service and the other workers. • Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting. • Retry failed items with backoff and record failures in structured logs. | Reads/updates job state records in the primary datastore; ensures idempotent task execution. |
| Ingest Worker | BackgroundWorker | • Run the ingest worker as its own background process, separate from the API service and the other workers. • Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting. • Retry failed items with backoff and record failures in structured logs. | Reads/updates job state records in the primary datastore; ensures idempotent task execution. |
| Scoring Worker | BackgroundWorker | • Run the scoring worker as its own background process, separate from the API service and the other workers. • Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting. • Retry failed items with backoff and record failures in structured logs. | Reads/updates job state records in the primary datastore; ensures idempotent task execution. |
| Web Client | ClientApp | • Provide responsive and accessible user interface for solution workflows. • Coordinate client-side state management, route transitions, and input validation. • Manage authentication sessions and handle operational error display. | Client-side reactive state managed in memory and browser storage (session tokens, preferences); no direct database access. Data sensitivity & client-side boundary: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat…. |
| Primary Database | DataStore | • Provide durable, ACID-compliant persistence for all domain entities and audit events. • Enforce relational integrity, foreign key constraints, and unique indexes. • Support point-in-time recovery and snapshot durability. | Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own). Data lifecycle and residency policy: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat…. |
| API / Backend Service | DeployableUnit | • Expose secure RESTful API endpoints for client and external consumers. • Enforce authentication, role-based authorization, and rate limiting. • Coordinate transactional unit-of-work across domain modules. • Emit structured audit logs and operational telemetry. | Coordinates database transactions across modules; manages connection lifetimes and migration application. |
| Data Quality | LogicalModule | • Implement core domain logic and invariant validation for: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.; Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.; Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |
| Release Health Analytics | LogicalModule | • Implement core domain logic and invariant validation for: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.; Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.; Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |

## 3. Entity Details & Data Governance Notes

### Digest Worker (BackgroundWorker)

- **Domain Responsibilities**: • Run the digest worker as its own background process, separate from the API service and the other workers.
• Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting.
• Retry failed items with backoff and record failures in structured logs.
- **Data Design & Schema Notes**: Reads/updates job state records in the primary datastore; ensures idempotent task execution.
- **API & Query Interface**: Internal job execution contract (a worker interface in the language of the chosen stack). Triggered via an in-process queue or timer schedule.
- **Boundary Rationale**: Dedicated background processing decouples resource-intensive or long-running tasks from user-facing request latency budgets.

### Ingest Worker (BackgroundWorker)

- **Domain Responsibilities**: • Run the ingest worker as its own background process, separate from the API service and the other workers.
• Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting.
• Retry failed items with backoff and record failures in structured logs.
- **Data Design & Schema Notes**: Reads/updates job state records in the primary datastore; ensures idempotent task execution.
- **API & Query Interface**: Internal job execution contract (a worker interface in the language of the chosen stack). Triggered via an in-process queue or timer schedule.
- **Boundary Rationale**: Dedicated background processing decouples resource-intensive or long-running tasks from user-facing request latency budgets.

### Scoring Worker (BackgroundWorker)

- **Domain Responsibilities**: • Run the scoring worker as its own background process, separate from the API service and the other workers.
• Take its work from the durable queue or schedule recorded in the technology and data decisions, and process each item at least once without double-counting.
• Retry failed items with backoff and record failures in structured logs.
- **Data Design & Schema Notes**: Reads/updates job state records in the primary datastore; ensures idempotent task execution.
- **API & Query Interface**: Internal job execution contract (a worker interface in the language of the chosen stack). Triggered via an in-process queue or timer schedule.
- **Boundary Rationale**: Dedicated background processing decouples resource-intensive or long-running tasks from user-facing request latency budgets.

### Web Client (ClientApp)

- **Domain Responsibilities**: • Provide responsive and accessible user interface for solution workflows.
• Coordinate client-side state management, route transitions, and input validation.
• Manage authentication sessions and handle operational error display.
- **Data Design & Schema Notes**: Client-side reactive state managed in memory and browser storage (session tokens, preferences); no direct database access. Data sensitivity & client-side boundary: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….
- **API & Query Interface**: Consumes HTTPS REST/JSON endpoints with token-based authorization. Handles RFC 7807 problem details and client-side error states.
- **Boundary Rationale**: Dedicated client presentation boundary decoupled from backend application logic to support independent UI updates and client-specific performance optimization.

### Primary Database (DataStore)

- **Domain Responsibilities**: • Provide durable, ACID-compliant persistence for all domain entities and audit events.
• Enforce relational integrity, foreign key constraints, and unique indexes.
• Support point-in-time recovery and snapshot durability.
- **Data Design & Schema Notes**: Relational database schema with versioned schema migrations. Indexed primary and foreign keys; created_at/updated_at audit columns on all primary tables. Technology decided for this component: SQLite (a technology decision, not a component of its own). Data lifecycle and residency policy: The data entities are deploy events from the CI system and incident events from the paging tool (service name, timestamp, outcome, change ticket id, severity); both exist today, are clean enough to score, and are owned by platform engineering, which maintains the webhook schema and its versioning. Data quality is validated on ingest: every webhook is checked against the documented schema, duplicat….
- **API & Query Interface**: Database access through the chosen data-access layer with connection pooling, command timeouts, and retry-on-failure strategies.
- **Boundary Rationale**: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.

### API / Backend Service (DeployableUnit)

- **Domain Responsibilities**: • Expose secure RESTful API endpoints for client and external consumers.
• Enforce authentication, role-based authorization, and rate limiting.
• Coordinate transactional unit-of-work across domain modules.
• Emit structured audit logs and operational telemetry.
- **Data Design & Schema Notes**: Coordinates database transactions across modules; manages connection lifetimes and migration application.
- **API & Query Interface**: HTTPS REST endpoints. Methods: GET, POST, PUT, DELETE. Bearer token authorization. Standard JSON request/response models with RFC 7807 problem details on error.
- **Boundary Rationale**: Core deployable boundary hosting API surface and domain logic as a cohesive Hybrid unit, balancing maintainability and deployment simplicity.

### Data Quality (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.; Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.; Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Data Design & Schema Notes**: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- **API & Query Interface**: In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.
- **Boundary Rationale**: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

### Release Health Analytics (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.; Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.; Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Data Design & Schema Notes**: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- **API & Query Interface**: In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.
- **Boundary Rationale**: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

## 4. Coding Agent Implementation Rules for TASK-001 (Database & Persistence)

When implementing database schema, migrations, and entities:
1. **Strict Boundary Conformance**: Implement only the tables, aggregates, and fields required by the domain specifications above and referenced requirements. Do not invent unapproved tables or bypass entity ownership boundaries.
2. **Auditability & Temporal Tracking**: Every primary persistence entity must include audit tracking fields (`CreatedAt`, `UpdatedAt`) and strong unique identifier keys (e.g. UUID/GUID or identity keys).
3. **Referential Integrity & Cascades**: Foreign keys must have explicit delete behaviors (avoid inadvertent cascading deletions on primary aggregates; use soft deletes or fail-closed foreign key checks where appropriate).
4. **Zero-Migration Loss**: Migrations must be additive, forward-compatible, and idempotent. Never mutate applied migrations in place.
5. **Data Protection & Classification**: Ensure restricted data, credentials, and PII are marked for encryption at rest and never logged in plain text.
