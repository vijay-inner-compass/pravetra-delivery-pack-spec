# Implementation Prompt

| Field | Value |
| --- | --- |
| Project / Pipeline | E03-focus-ledger |
| Artifact version | 1 |
| Generated | 2026-10-09 11:34:13Z |
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

- **Problem:** Independent consultants and freelance developers who bill by the hour lose track of how much real focused work they do. They estimate their week from memory, under-bill by an average of 4 to 6 hours a week, and cannot see which kinds of work eat their time. Existing cloud time trackers want an account and upload task names and client names to a server, which several of our target users refuse for client-confidentiality reasons.
- **Proposed solution:** A small .NET desktop application called Focus Ledger. The user starts a focus session with a client and a one-line task, the app shows a tray timer, prompts after 90 minutes of inactivity to confirm or trim the session, and stores everything in an encrypted local database. A weekly review screen totals sessions by client and task type, and the user can export a CSV or PDF timesheet. Nothing leaves the machine unless the user exports a file.
- **Business value:** Recover the 4 to 6 hours a week that go unbilled and give each user a trustworthy weekly timesheet in one click. Target: unbilled time under 1 hour a week for pilot users, and a Friday timesheet in under 2 minutes.
- **Approved technology approach:** traditional_software — The proposed solution, a .NET desktop application called Focus Ledger, is best categorized as a traditional software application. It addresses the specific needs of independent consultants and freelancers by providing a reliable, offline timer that tracks billable hours without requiring cloud connectivity. While workflow automation and rules engines could streamline some processes, they do not adequately address the core problem of accurately tracking time in a user-friendly manner. Workflow automation would not capture the necessary offline functionality and real-time tracking, while a rules engine would not provide the intuitive interface needed for users to start and stop timers easily. The deterministic nature of the problem allows for a straightforward software solution without the complexities introduced by AI.

## 2. Executive Summary

| Metric | Value |
| --- | --- |
| Decided technology choices | 3 |
| Accepted ADRs | 3 |
| Ready requirement prompts | 21 |
| Skipped requirements | 0 |

## 3. Project Technology Decisions

Apply these wherever relevant to a requirement below — they are project-wide, not tied to one specific requirement.

- **Selected option:** C# on .NET 10 with the Avalonia UI desktop toolkit
  - Options considered: C# on .NET 10 with the Avalonia UI desktop toolkit vs WPF (Windows only, so it cannot run on the owner's Mac) vs .NET MAUI (no Linux support and weaker desktop support than Avalonia) vs WinForms (Windows only) vs A local web page or an Electron shell (not .NET, and a local port is a network surface the no-network promise forbids) vs Python with a Qt or Tkinter toolkit (rejected: the owner mandates .NET for all three examples)
  - Rejected alternatives (do not use): WPF (Windows only, so it cannot run on the owner's Mac); .NET MAUI (no Linux support and weaker desktop support than Avalonia); WinForms (Windows only); A local web page or an Electron shell (not .NET, and a local port is a network surface the no-network promise forbids); Python with a Qt or Tkinter toolkit (rejected: the owner mandates .NET for all three examples)
  - Rationale: Application language and desktop UI toolkit. The owner mandates .NET. Avalonia UI gives a real native window, a system tray icon and a timer on Windows, macOS and Linux from one codebase, which matches the owner's Mac and the Windows target; the tray timer requires a tray icon. The app is published as a single-file, self-contained executable per platform (dotnet publish) and tested with xUnit.
  - Benefits: One codebase runs on macOS, Windows and Linux; the owner already works in .NET.
  - Disadvantages: Fewer ready-made controls than WPF; a smaller community than web toolkits.
- **Selected option:** an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite
  - Options considered: an embedded SQLite database file, one per user, on the user machine, accessed through Microsoft.Data.Sqlite vs plain JSON or CSV files in a user folder (no transactions, so a crash mid-write corrupts the ledger)
  - Rejected alternatives (do not use): plain JSON or CSV files in a user folder (no transactions, so a crash mid-write corrupts the ledger)
  - Rationale: Database. SQLite is the mandated database. It is a single file with no server process, so the product keeps its local-first, no-server promise and a backup is a file copy.
  - Benefits: Transactions protect the ledger from a crash mid-write; one file is easy to back up and restore.
  - Disadvantages: Encryption at rest needs an encrypted SQLite build or equivalent.
- **Selected option:** CSV export
  - Options considered: CSV export vs PDF export
  - Rejected alternatives (do not use): PDF export
  - Rationale: The choice between CSV and PDF export depends on user needs for data presentation. CSV is favored for its simplicity, while PDF is preferred for formal documentation.
  - Benefits: No extra library; opens in any spreadsheet; suits billing and invoicing.
  - Disadvantages: No formatting or branding; PDF is not offered in the first version.

## 4. Accepted ADRs


## 5. Per-Requirement Implementation Prompts

Ordered business requirements first, then functional, then non-functional; Must priority before Should before Could within each.

### Requirement 1 of 21 — business, Must priority

**Implement:** Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.

### Requirement 2 of 21 — business, Must priority

**Implement:** Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.

### Requirement 3 of 21 — functional, Must priority

**Implement:** The application must allow users to start a focus session by selecting a client and entering a one-line task description.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to start a focus session by selecting a client and entering a one-line task description.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 4 of 21 — functional, Must priority

**Implement:** The application must display a timer in the system tray that counts the duration of the focus session.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must display a timer in the system tray that counts the duration of the focus session.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 5 of 21 — functional, Must priority

**Implement:** The application must prompt the user after 90 minutes of inactivity to confirm whether to continue the session or trim it.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must prompt the user after 90 minutes of inactivity to confirm whether to continue the session or trim it.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 6 of 21 — functional, Must priority

**Implement:** The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 7 of 21 — functional, Must priority

**Implement:** The application must provide a weekly review screen that totals sessions by client and task type.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must provide a weekly review screen that totals sessions by client and task type.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 8 of 21 — functional, Must priority

**Implement:** The application must allow users to export their timesheet as a CSV or PDF file.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to export their timesheet as a CSV or PDF file.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 9 of 21 — functional, Must priority

**Implement:** The application must allow users to manually stop a focus session and record the end time.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to manually stop a focus session and record the end time.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 10 of 21 — functional, Must priority

**Implement:** The application must allow users to view a history of their past focus sessions, including client names, task descriptions, and duration.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to view a history of their past focus sessions, including client names, task descriptions, and duration.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 11 of 21 — functional, Should priority

**Implement:** The application must notify users of any unsaved session data when they attempt to close the application.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must notify users of any unsaved session data when they attempt to close the application.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 12 of 21 — functional, Should priority

**Implement:** The application must provide a mechanism for users to edit or delete past focus sessions.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The application must provide a mechanism for users to edit or delete past focus sessions.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 13 of 21 — nonfunctional, Must priority

**Implement:** The application must ensure that the timer updates in real-time with a maximum latency of 1 second.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that the timer updates in real-time with a maximum latency of 1 second.

### Requirement 14 of 21 — nonfunctional, Must priority

**Implement:** The application must start and record focus sessions without a network connection, so the timer is available whenever the user's computer is on.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must maintain an availability of 99.9% during the pilot phase, ensuring that users can access the timer functionality at all times.

### Requirement 15 of 21 — nonfunctional, Must priority

**Implement:** The application must encrypt all stored data at rest using AES-256 encryption to protect sensitive client information.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must encrypt all stored data at rest using AES-256 encryption to protect sensitive client information.

### Requirement 16 of 21 — nonfunctional, Must priority

**Implement:** The application must provide a backup and recovery mechanism that allows users to restore their session data from an encrypted local backup file.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must provide a backup and recovery mechanism that allows users to restore their session data from an encrypted local backup file.

### Requirement 17 of 21 — nonfunctional, Must priority

**Implement:** The application must comply with GDPR regulations, allowing users to delete their data upon request.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must comply with GDPR regulations, allowing users to delete their data upon request.

### Requirement 18 of 21 — nonfunctional, Must priority

**Implement:** The application must ensure that session data is backed up at least once a week to prevent data loss.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that session data is backed up at least once a week to prevent data loss.

### Requirement 19 of 21 — nonfunctional, Should priority

**Implement:** The application must allow users to access their historical session data for as long as they keep it.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must allow for data retention of at least 5 years, enabling users to access historical session data.

### Requirement 20 of 21 — nonfunctional, Should priority

**Implement:** The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.

### Requirement 21 of 21 — nonfunctional, Should priority

**Implement:** The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.

## 7. Handoff Guidance

- Use this artifact as implementation input only after acceptance criteria and architecture drivers are reviewed.
- Regenerate when requirements, ADRs, or technology decisions change.
