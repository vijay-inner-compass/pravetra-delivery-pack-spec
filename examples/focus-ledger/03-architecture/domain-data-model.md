# Domain Data Model & Entity Dictionary

This document specifies the **Domain Data Model, Entity Boundaries, and Schema Requirements** for **E03-focus-ledger**. It provides the persistence models, aggregate roots, relationships, and data governance rules required for autonomous coding agents implementing **TASK-001 (Primary Database / Persistence)** and component domain services across **Domain-Driven Design (DDD)**, **Scrum Data Modeling**, **SAFe Architecture Enablers**, and **Enterprise Database Engineering**.

## 1. Architecture & Persistence Context

| Architecture Attribute | Specification |
| --- | --- |
| Architecture Style | Modular Monolith |
| Decomposition Structure | ModularMonolith |
| Target Schema Version | v2 |

### Decided Persistence Stack

- **Technology**: C# on .NET 10 with the Avalonia UI desktop toolkit (rejected alternatives, do not use: WPF (Windows only, so it cannot run on the owner's Mac); .NET MAUI (no Linux support and weaker desktop support than Avalonia); WinForms (Windows only); A local web page or an Electron shell (not .NET, and a local port is a network surface the no-network promise forbids); Python with a Qt or Tkinter toolkit (rejected: the owner mandates .NET for all three examples)). Rationale: Application language and desktop UI toolkit. The owner mandates .NET. Avalonia UI gives a real native window, a system tray icon and a timer on Windows, macOS and Linux from one codebase, which matches the owner's Mac and the Windows target; the tray timer requires a tray icon. The app is published as a single-file, self-contained executable per platform (dotnet publish) and tested with xUnit.
- **Technology**: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (rejected alternatives, do not use: plain JSON or CSV files in a user folder (no transactions, so a crash mid-write corrupts the ledger)). Rationale: Database. SQLite is the mandated database. It is a single file with no server process, so the product keeps its local-first, no-server promise and a backup is a file copy.
- **Technology**: CSV export (rejected alternatives, do not use: PDF export). Rationale: The choice between CSV and PDF export depends on user needs for data presentation. CSV is favored for its simplicity, while PDF is preferred for formal documentation.

## 2. Component Entity & Schema Specifications

| Component | Kind | Responsibilities | Data Design & Entities |
| --- | --- | --- | --- |
| Desktop Client | ClientApp | • Provide the desktop user interface and its keyboard, window and file-dialog behaviour for the target operating systems. • Run the domain modules in-process on the user's machine; no network service is involved. • Keep window and view state locally; every durable fact goes through the local data store. | Holds transient interface state only; all durable data is read and written through the local data store. |
| Local Encrypted Database | DataStore | • Persist the application's data in a single local database file on the user's machine. • Protect the data at rest as the confirmed data decision requires (for example encryption, with the key kept in the operating-system key store). • Support backup and restore of the one file, and versioned local schema upgrades when the application is updated. | Embedded relational schema with versioned local upgrades; the file is created on first run and never leaves the user's machine unless the user exports it. |
| Session Tracking | LogicalModule | • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |
| Timesheet and Export | LogicalModule | • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. | Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation. |

## 3. Entity Details & Data Governance Notes

### Desktop Client (ClientApp)

- **Domain Responsibilities**: • Provide the desktop user interface and its keyboard, window and file-dialog behaviour for the target operating systems.
• Run the domain modules in-process on the user's machine; no network service is involved.
• Keep window and view state locally; every durable fact goes through the local data store.
- **Data Design & Schema Notes**: Holds transient interface state only; all durable data is read and written through the local data store.
- **API & Query Interface**: No network API. The client calls the domain modules in-process; import and export file formats, if any, are recorded here.
- **Boundary Rationale**: Dedicated client presentation boundary decoupled from backend application logic to support independent UI updates and client-specific performance optimization.

### Local Encrypted Database (DataStore)

- **Domain Responsibilities**: • Persist the application's data in a single local database file on the user's machine.
• Protect the data at rest as the confirmed data decision requires (for example encryption, with the key kept in the operating-system key store).
• Support backup and restore of the one file, and versioned local schema upgrades when the application is updated.
- **Data Design & Schema Notes**: Embedded relational schema with versioned local upgrades; the file is created on first run and never leaves the user's machine unless the user exports it.
- **API & Query Interface**: Accessed only through the domain modules, in-process, through the embedded database driver; no network access.
- **Boundary Rationale**: Centralized relational database ensures ACID transaction guarantees and cross-module relational consistency without complex distributed transactions.

### Session Tracking (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description..
• Validate command inputs and orchestrate state transitions.
• Emit domain notifications and audit events upon state changes.
- **Data Design & Schema Notes**: Owns domain entities and aggregate roots. Enforces relational schema constraints and entity validation.
- **API & Query Interface**: In-process service contracts and interfaces written in the language of the stack chosen for this project. Typed request/response models, explicit success-or-failure results, and cancellation or timeout support where the chosen language offers it.
- **Boundary Rationale**: Logical module boundary encapsulates bounded domain invariants and prevents leaky abstractions without premature network serialization overhead.

### Timesheet and Export (LogicalModule)

- **Domain Responsibilities**: • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description..
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
