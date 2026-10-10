# Architecture Summary

| Field | Value |
| --- | --- |
| Architecture style | Modular Monolith |
| Decomposition | ModularMonolith |
| Branching strategy | Trunk-based development |

Rationale: A single deployable unit keeps operational overhead low while the project's current scope stays small.

## Selected Technology

- **Technology**: C# on .NET 10 with the Avalonia UI desktop toolkit (rejected alternatives, do not use: WPF (Windows only, so it cannot run on the owner's Mac); .NET MAUI (no Linux support and weaker desktop support than Avalonia); WinForms (Windows only); A local web page or an Electron shell (not .NET, and a local port is a network surface the no-network promise forbids); Python with a Qt or Tkinter toolkit (rejected: the owner mandates .NET for all three examples)). Rationale: Application language and desktop UI toolkit. The owner mandates .NET. Avalonia UI gives a real native window, a system tray icon and a timer on Windows, macOS and Linux from one codebase, which matches the owner's Mac and the Windows target; the tray timer requires a tray icon. The app is published as a single-file, self-contained executable per platform (dotnet publish) and tested with xUnit.
- **Technology**: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite (rejected alternatives, do not use: plain JSON or CSV files in a user folder (no transactions, so a crash mid-write corrupts the ledger)). Rationale: Database. SQLite is the mandated database. It is a single file with no server process, so the product keeps its local-first, no-server promise and a backup is a file copy.
- **Technology**: CSV export (rejected alternatives, do not use: PDF export). Rationale: The choice between CSV and PDF export depends on user needs for data presentation. CSV is favored for its simplicity, while PDF is preferred for formal documentation.

## Component Catalog

| Component | Kind | Responsibilities |
| --- | --- | --- |
| Desktop Client | ClientApp | • Provide the desktop user interface and its keyboard, window and file-dialog behaviour for the target operating systems. • Run the domain modules in-process on the user's machine; no network service is involved. • Keep window and view state locally; every durable fact goes through the local data store. |
| Local Encrypted Database | DataStore | • Persist the application's data in a single local database file on the user's machine. • Protect the data at rest as the confirmed data decision requires (for example encryption, with the key kept in the operating-system key store). • Support backup and restore of the one file, and versioned local schema upgrades when the application is updated. |
| Session Tracking | LogicalModule | • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |
| Timesheet and Export | LogicalModule | • Implement core domain logic and invariant validation for: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.; Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.; The application must allow users to start a focus session by selecting a client and entering a one-line task description.. • Validate command inputs and orchestrate state transitions. • Emit domain notifications and audit events upon state changes. |

