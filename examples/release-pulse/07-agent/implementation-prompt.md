# Implementation Prompt

| Field | Value |
| --- | --- |
| Project / Pipeline | E02-release-pulse |
| Artifact version | 1 |
| Generated | 2026-10-09 10:53:23Z |
| Document status | Current at generation time |
| Classification | Internal project delivery artifact |
| Review posture | Draft until reviewed and accepted by accountable project roles |

> This artifact is generated from captured Pravetra project data. Empty sections are intentionally marked instead of inferred.

---


This document is a self-contained implementation brief for a coding agent. Read the project context and the technology decisions below before writing any code. Then implement each requirement in the order listed, satisfying every one of its acceptance criteria and honoring any architecture driver, technology decision, or ADR that applies to it.

### Strict Grounding & Execution Rules
- **No Invented Services:** Ground implementation strictly in the confirmed technology decisions and ADRs below. Do not add external cloud services, third-party databases, or unmentioned frameworks.
- **Honor Locked Decisions:** User mandates and decided technology choices are authoritative and immutable. If codebase reality contradicts them, stop and report a contradiction rather than assuming alternative technologies.
- **Negative Paths & Boundaries:** Satisfy both normal workflows and exceptional/negative validation conditions defined in acceptance criteria.
- **Zero Silent Assumptions:** Never make silent architectural choices for uncaptured requirements.

## 1. Project Context

- **Problem:** Engineering managers at our 14-team product group cannot tell, before Monday planning, which services had risky releases last week. Deploy events sit in the CI system, incidents sit in the paging tool, and rollbacks sit in chat. Each Monday a manager spends about 90 minutes assembling this by hand, and two incidents last quarter were repeats of a risky release pattern nobody had connected.
- **Proposed solution:** The proposed solution is a .NET web application named Release Pulse, which integrates seamlessly into existing operations by connecting to the CI system and the incident tracking tool through webhooks. The ingest API will receive deploy and incident data in real-time, while three hosted background workers will process this data: the ingest worker will normalize incoming events, the scoring worker will calculate the release-health score based on defined rules, and the digest worker will compile and email a summary to each manager every Monday morning. This automation eliminates the manual assembly process, providing a consistent and trustworthy view of release health.
- **Business value:** Give every manager a consistent, trustworthy weekly release-health view in under one minute instead of 90 minutes of spreadsheet work, and surface repeated risky patterns before they become incidents. Target: 14 of 14 teams on the same weekly view, and no manual assembly after the first month.
- **Approved technology approach:** traditional_software — The proposed solution is a .NET web application that integrates with existing systems to automate the data aggregation process. While workflow automation could streamline some aspects of the process, it lacks the necessary real-time data processing capabilities and would still require manual intervention for scoring and reporting. A rules engine could provide deterministic scoring, but it would not address the need for a comprehensive view of release health across multiple teams. The traditional software approach allows for tailored functionality that meets the specific needs of the engineering managers without the limitations of simpler alternatives.

## 2. Executive Summary

| Metric | Value |
| --- | --- |
| Decided technology choices | 3 |
| Accepted ADRs | 3 |
| Ready requirement prompts | 19 |
| Skipped requirements | 0 |

## 3. Project Technology Decisions

Apply these wherever relevant to a requirement below — they are project-wide, not tied to one specific requirement.

- **Selected option:** C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process
  - Options considered: C# on .NET: an ASP.NET Core API that also hosts the three background workers (ingest, scoring, digest) as hosted background services in one process vs Python workers beside a .NET API (a second runtime to build, deploy and monitor) vs Three separate .NET worker processes (three deployments for one small team group)
  - Rejected alternatives (do not use): Python workers beside a .NET API (a second runtime to build, deploy and monitor); Three separate .NET worker processes (three deployments for one small team group)
  - Rationale: Server language, framework and hosting model. The owner mandates .NET. One process keeps deployment to a single published build, and hosted services give the workers a lifetime tied to the API host without a second runtime.
  - Benefits: One deployment and one runtime. The workers share the API's configuration and logging.
  - Disadvantages: A worker fault can affect the API host. Workers scale with the API, not separately.
- **Selected option:** a SQLite-backed job table polled by the hosted background services
  - Options considered: a SQLite-backed job table polled by the hosted background services vs an in-process channel (System.Threading.Channels) inside the API host (events queued in memory are lost when the host restarts) vs a spool folder of JSON files read by the workers (no transactions; a crash can lose or double-process an event)
  - Rejected alternatives (do not use): an in-process channel (System.Threading.Channels) inside the API host (events queued in memory are lost when the host restarts); a spool folder of JSON files read by the workers (no transactions; a crash can lose or double-process an event)
  - Rationale: Database and background-work queue. SQLite is the mandated database. A job table written in the same transaction as the event makes the at-least-once, scored-once requirement testable, with no broker to run. Write-ahead mode lets the API read while a worker writes.
  - Benefits: The event and its job are written in one transaction, so a crash cannot lose an accepted event. No broker to run.
  - Disadvantages: One writer at a time. Throughput suits 14 managers, not thousands of teams.
- **Selected option:** ASP.NET Core Web API with polling mechanism
  - Options considered: ASP.NET Core Web API with SignalR vs ASP.NET Core Web API with polling mechanism
  - Rejected alternatives (do not use): ASP.NET Core Web API with SignalR
  - Rationale: The choice between SignalR and polling hinges on the need for real-time updates versus simplicity. SignalR offers a more responsive user experience, which aligns with the requirement for timely insights, but comes with added complexity. Polling is easier to implement but may not meet the latency requirements effectively.
  - Benefits: Using SignalR allows for real-time updates to the web client, providing immediate visibility into release health changes. This enhances user experience by delivering insights without requiring manual refreshes. Polling can be simpler to implement and does not require additional configuration for real-time communication.
  - Disadvantages: SignalR introduces additional complexity in managing real-time connections and may require more resources for scaling. Polling can lead to increased load on the server and may not provide timely updates if the polling interval is too long.

## 4. Accepted ADRs

- **Context:** The service needs an API, three background workers and a web client for a small team group.
  - Decision: Use C# on .NET: an ASP.NET Core API that also hosts the three background workers as hosted services in one process.
  - Consequences: One thing to build, deploy and monitor. A worker fault can affect the API host.
- **Context:** Webhook events must not be lost when a worker restarts, and the mandate is SQLite only.
  - Decision: Use SQLite for storage and a SQLite-backed job table polled by the hosted background services as the queue.
  - Consequences: Accepted events are durable. Single-writer throughput must be watched.
- **Context:** The web client must show the weekly release-health view and refresh as scores change.
  - Decision: Use an ASP.NET Core Web API with polling: the client refreshes the view every 30 to 60 seconds.
  - Consequences: Simple and robust. Updates appear within one polling interval.

## 5. Per-Requirement Implementation Prompts

Ordered business requirements first, then functional, then non-functional; Must priority before Should before Could within each.

### Requirement 1 of 19 — business, Must priority

**Implement:** Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Provide a consistent, trustworthy weekly release-health view for all 14 engineering managers, reducing the manual assembly time from 90 minutes to under one minute by automating data aggregation.

### Requirement 2 of 19 — business, Must priority

**Implement:** Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Surface repeated risky release patterns before they escalate into incidents, ensuring that all managers are aware of potential issues in a timely manner.

### Requirement 3 of 19 — business, Must priority

**Implement:** Ensure that the application provides insights into the release health of each service, allowing for comparisons across teams.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the application provides insights into the release health of each service, allowing for comparisons across teams.

### Requirement 4 of 19 — functional, Must priority

**Implement:** Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Integrate with the CI system to receive deploy events in real-time via webhooks, capturing service name, timestamp, outcome, and change ticket ID for each deploy.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 5 of 19 — functional, Must priority

**Implement:** Integrate with the incident tracking tool to receive incident events in real-time via webhooks, capturing service name, timestamp, severity, and other relevant details.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Integrate with the incident tracking tool to receive incident events in real-time via webhooks, capturing service name, timestamp, severity, and other relevant details.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 6 of 19 — functional, Must priority

**Implement:** Normalize incoming deploy and incident data to ensure consistency across all teams, applying defined rules for scoring release health.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Normalize incoming deploy and incident data to ensure consistency across all teams, applying defined rules for scoring release health.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 7 of 19 — functional, Must priority

**Implement:** Calculate a release-health score based on defined rules, updating the score in real-time as new deploy and incident data is ingested.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Calculate a release-health score based on defined rules, updating the score in real-time as new deploy and incident data is ingested.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 8 of 19 — functional, Must priority

**Implement:** Compile a summary of release health for each team and email it to all engineering managers every Monday morning, ensuring timely delivery of insights.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Compile a summary of release health for each team and email it to all engineering managers every Monday morning, ensuring timely delivery of insights.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 9 of 19 — functional, Must priority

**Implement:** Implement role-based access control for engineering managers and on-call engineers to ensure appropriate permissions for viewing release health data.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Implement role-based access control for engineering managers and on-call engineers to ensure appropriate permissions for viewing release health data.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 10 of 19 — functional, Must priority

**Implement:** Allow engineering managers to compare release health scores across different teams within the user interface.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Allow engineering managers to compare release health scores across different teams within the user interface.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 11 of 19 — functional, Should priority

**Implement:** Provide a user interface that allows engineering managers to view the release health summary and drill down into specific incidents and deploy events.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Provide a user interface that allows engineering managers to view the release health summary and drill down into specific incidents and deploy events.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 12 of 19 — functional, Should priority

**Implement:** Provide notifications to on-call engineers when a deploy event is associated with a high-severity incident, ensuring they are informed of potential issues.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: Provide notifications to on-call engineers when a deploy event is associated with a high-severity incident, ensuring they are informed of potential issues.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 13 of 19 — nonfunctional, Must priority

**Implement:** Ensure the application is available during working hours, with monitoring in place to detect and alert on any downtime.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Ensure the application has an availability target of 99.9%, with monitoring in place to detect and alert on any downtime.

### Requirement 14 of 19 — nonfunctional, Must priority

**Implement:** Process incoming webhook events with a latency of no more than 2 seconds for 95% of events, ensuring timely updates to release health scores.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Process incoming webhook events with a latency of no more than 2 seconds for 95% of events, ensuring timely updates to release health scores.

### Requirement 15 of 19 — nonfunctional, Must priority

**Implement:** Implement data encryption in transit and at rest to protect sensitive incident data, ensuring compliance with internal security policies.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Implement data encryption in transit and at rest to protect sensitive incident data, ensuring compliance with internal security policies.

### Requirement 16 of 19 — nonfunctional, Must priority

**Implement:** Maintain an audit log of all actions taken within the application, including data ingestion, scoring calculations, and user access, retaining logs for a minimum of 24 months.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Maintain an audit log of all actions taken within the application, including data ingestion, scoring calculations, and user access, retaining logs for a minimum of 24 months.

### Requirement 17 of 19 — nonfunctional, Must priority

**Implement:** Ensure the application complies with internal data protection policies, including data retention and access controls.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Ensure the application complies with internal data protection policies, including data retention and access controls.

### Requirement 18 of 19 — nonfunctional, Should priority

**Implement:** Ensure the application is scalable to handle increased data volumes as the number of deploys and incidents grows, with a target of supporting at least 1000 events per hour.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Ensure the application is scalable to handle increased data volumes as the number of deploys and incidents grows, with a target of supporting at least 1000 events per hour.

### Requirement 19 of 19 — nonfunctional, Should priority

**Implement:** Ensure the application is maintainable, allowing for updates and modifications without significant downtime or disruption to service.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: Ensure the application is maintainable, allowing for updates and modifications without significant downtime or disruption to service.

## 7. Handoff Guidance

- Use this artifact as implementation input only after acceptance criteria and architecture drivers are reviewed.
- Regenerate when requirements, ADRs, or technology decisions change.
