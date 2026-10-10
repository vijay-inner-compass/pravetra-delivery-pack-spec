# Domain & Terminology

> Canonical policy version: blueprint-v2-tasks-23-15bea665
> Generated: 2026-10-09 11:48:57Z
> Project: E03-focus-ledger
Architecture style: Modular Monolith.

Components:

| Component | Kind | Responsibilities |
| --- | --- | --- |
| Desktop Client | ClientApp | • Provide the desktop user interface and its keyboard, window and file-dialog behaviour for the target operating systems. • Run the domain modules in-process on the user's machine; no network service is involved. • Keep window and view state locally; every durable fact goes through the local data store. |
| Local Encrypted Database | DataStore | • Persist the application's data in a single local database file on the user's machine. • Protect the data at rest as the confirmed data decision requires (for example encryption, with the key kept in the operating-system key store). • Support backup and restore of the one file, and versioned local schema upgrades when the application is updated. |
| Session Tracking | LogicalModule | • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Timesheet and Export | LogicalModule | • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |

