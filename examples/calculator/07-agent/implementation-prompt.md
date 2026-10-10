# Implementation Prompt

| Field | Value |
| --- | --- |
| Project / Pipeline | E01-calculator |
| Artifact version | 1 |
| Generated | 2026-10-09 09:38:52Z |
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

- **Problem:** Our 6-person finance operations team checks invoice totals, tax and discount arithmetic by hand or in ad-hoc spreadsheets and makes frequent mistakes, especially with operator precedence, rounding and division by zero. We need a small, trustworthy calculator that the team runs from a terminal. No other teams or systems are affected.
- **Proposed solution:** To resolve the problem of frequent arithmetic errors in invoice totals, we propose developing a command-line calculator in C# on .NET 10 that will run locally on each analyst's laptop. The tool will evaluate arithmetic expressions with proper operator precedence, handle rounding using decimal arithmetic, and maintain a local SQLite database to store the last 10 calculations. This solution integrates seamlessly into existing operations by allowing analysts to input invoice numbers directly into the terminal, receive accurate results, and access their calculation history without needing to change their current workflow of using terminals.
- **Business value:** Cut invoice-total arithmetic errors from about 5% of checked totals to under 0.5%, and cut rework time from roughly 30 minutes per wrong total to near zero. Measured monthly by the team lead from the count of corrected invoices.
- **Approved technology approach:** traditional_software — The proposed solution of a command-line calculator is categorized as 'traditional_software' because it directly addresses the arithmetic errors in invoice totals through deterministic logic. While a 'rules_engine' could also enforce arithmetic rules, it would not provide the same level of user control and simplicity that a dedicated calculator offers. The complexity of implementing a rules engine for this specific use case, where the primary need is accurate arithmetic evaluation, does not justify its use. The traditional software approach ensures that the team can input calculations directly and receive immediate feedback, which is essential for their daily operations.

## 2. Executive Summary

| Metric | Value |
| --- | --- |
| Decided technology choices | 6 |
| Accepted ADRs | 6 |
| Ready requirement prompts | 23 |
| Skipped requirements | 0 |

## 3. Project Technology Decisions

Apply these wherever relevant to a requirement below — they are project-wide, not tied to one specific requirement.

- **Selected option:** C# on .NET 10 as a console application, tested with xUnit
  - Options considered: C# on .NET 10 as a console application, tested with xUnit vs Python 3 script tested with pytest (the team knows .NET; a Python runtime would have to be installed on analyst laptops) vs F# on .NET 10 (no team experience)
  - Rejected alternatives (do not use): Python 3 script tested with pytest (the team knows .NET; a Python runtime would have to be installed on analyst laptops); F# on .NET 10 (no team experience)
  - Rationale: Implementation language and test framework. The team already knows C# and .NET, and System.Decimal avoids the binary floating-point errors that are the core problem. The owner mandates .NET for the showcase.
  - Benefits: The team already knows C#. System.Decimal is exact for money. One small executable. xUnit is mature.
  - Disadvantages: Needs the .NET runtime, or a larger self-contained build.
- **Selected option:** an embedded SQLite database file accessed with Microsoft.Data.Sqlite
  - Options considered: an embedded SQLite database file accessed with Microsoft.Data.Sqlite vs a JSON file rewritten after every calculation (no transactions; a crash mid-write corrupts the history) vs a plain-text file with one line per calculation (same weakness, and no way to enforce the last-10 rule atomically)
  - Rejected alternatives (do not use): a JSON file rewritten after every calculation (no transactions; a crash mid-write corrupts the history); a plain-text file with one line per calculation (same weakness, and no way to enforce the last-10 rule atomically)
  - Rationale: Storage for the calculation history. SQLite is the mandated database. It gives transactional writes, survives a crash mid-write, needs no server and is one file to back up or delete.
  - Benefits: No server. Transactional writes survive a crash mid-write. One file. Works on Windows, macOS and Linux.
  - Disadvantages: One writer at a time. History lives only on each analyst's laptop.
- **Selected option:** System.Decimal for arithmetic operations
  - Options considered: System.Decimal for arithmetic operations vs double for arithmetic operations
  - Rejected alternatives (do not use): double for arithmetic operations
  - Rationale: System.Decimal is the preferred choice for this project due to its ability to handle financial calculations accurately. The requirement for precise arithmetic evaluation (R10) and the need to avoid floating-point inaccuracies make System.Decimal the only viable option. Switching to double would compromise the integrity of the calculations, which is unacceptable given the project's goals.
  - Benefits: System.Decimal provides high precision for financial calculations, avoiding floating-point inaccuracies. It ensures accurate rounding and operator precedence, which is critical for invoice totals. Using double may lead to rounding errors and inaccuracies in financial computations.
  - Disadvantages: System.Decimal may have slightly slower performance compared to double due to its higher precision and complexity in calculations. Using double can lead to unexpected results in financial contexts, which is unacceptable for this application.
- **Selected option:** Console.ReadLine for user input
  - Options considered: Console.ReadLine for user input vs Command-line arguments for user input
  - Rejected alternatives (do not use): Command-line arguments for user input
  - Rationale: Both input methods are viable, but Console.ReadLine is preferred for its simplicity and direct interaction with users. Command-line arguments can be considered for advanced use cases where batch processing is needed.
  - Benefits: Console.ReadLine allows for interactive input directly in the terminal, making it user-friendly. Command-line arguments can facilitate batch processing or scripting, allowing users to input multiple expressions at once.
  - Disadvantages: Console.ReadLine requires the user to input expressions one at a time, which may slow down workflows. Command-line arguments may complicate usage for less technical users and require additional documentation.
- **Selected option:** Decimal rounding for results
  - Options considered: Decimal rounding for results vs String formatting for output
  - Rejected alternatives (do not use): String formatting for output
  - Rationale: Decimal rounding is essential for financial accuracy, while string formatting enhances user experience. Both should be implemented to ensure the calculator meets its functional requirements.
  - Benefits: Decimal rounding ensures that results are accurate to the required precision. String formatting allows for flexible display options, making results easier to read.
  - Disadvantages: Decimal rounding may require additional logic to implement correctly. String formatting may introduce complexity in ensuring consistent output across different operations.
- **Selected option:** Console.Error for error messages
  - Options considered: Console.Error for error messages vs Throwing exceptions for error handling
  - Rejected alternatives (do not use): Throwing exceptions for error handling
  - Rationale: Both options provide mechanisms for handling errors gracefully, but using Console.Error aligns with the requirement for clear user feedback without crashing the application.
  - Benefits: Using Console.Error allows for clear visibility of error messages directly in the terminal, while throwing exceptions can provide detailed stack traces for debugging.
  - Disadvantages: Console.Error may not provide structured error handling, and throwing exceptions could lead to application crashes if not handled properly.

## 4. Accepted ADRs

- **Context:** Malformed input must give clear feedback without crashing.
  - Decision: Write clear messages to Console.Error and return a non-zero exit code.
  - Consequences: Callers and scripts can detect failure by the exit code.
- **Context:** The calculator must keep the last 10 calculations on each laptop with no server.
  - Decision: Use an embedded SQLite database file accessed with Microsoft.Data.Sqlite.
  - Consequences: Single-writer, local-only history. Parameterised SQL is mandatory.
- **Context:** The calculator needs one implementation language and test framework.
  - Decision: Use C# on .NET 10 as a console application, tested with xUnit.
  - Consequences: One stack to build and operate. Needs the .NET runtime or a self-contained build.
- **Context:** Results must be accurate to the required precision.
  - Decision: Round results with decimal rounding; formatting is a display detail.
  - Consequences: The rounding mode must be documented and covered by tests.
- **Context:** Invoice totals need exact arithmetic.
  - Decision: Use System.Decimal for all arithmetic.
  - Consequences: Exact results; slightly slower than double, which does not matter here.
- **Context:** The analyst types expressions into the terminal.
  - Decision: Read expressions interactively with Console.ReadLine.
  - Consequences: Simple interaction; no argument parsing needed for the first release.

## 5. Per-Requirement Implementation Prompts

Ordered business requirements first, then functional, then non-functional; Must priority before Should before Could within each.

### Requirement 1 of 23 — business, Must priority

**Implement:** Reduce the error rate in invoice total calculations from approximately 5% to under 0.5% by implementing a command-line calculator.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Reduce the error rate in invoice total calculations from approximately 5% to under 0.5% by implementing a command-line calculator.

### Requirement 2 of 23 — business, Must priority

**Implement:** Minimize rework time associated with incorrect invoice totals from roughly 30 minutes per error to near zero.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Minimize rework time associated with incorrect invoice totals from roughly 30 minutes per error to near zero.

### Requirement 3 of 23 — business, Must priority

**Implement:** Ensure the command-line calculator is compatible with Windows, macOS, and Linux operating systems.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure the command-line calculator is compatible with Windows, macOS, and Linux operating systems.

### Requirement 4 of 23 — business, Must priority

**Implement:** Ensure the command-line calculator provides accurate results for various arithmetic operations, including addition, subtraction, multiplication, and division.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure the command-line calculator provides accurate results for various arithmetic operations, including addition, subtraction, multiplication, and division.

### Requirement 5 of 23 — business, Should priority

**Implement:** Ensure that the command-line calculator is user-friendly and requires minimal training for the finance operations analysts.

**Acceptance criteria (all must pass before this is done):**
- Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Ensure that the command-line calculator is user-friendly and requires minimal training for the finance operations analysts.

### Requirement 6 of 23 — functional, Must priority

**Implement:** The calculator shall evaluate arithmetic expressions with proper operator precedence, ensuring that expressions like '100 - 10% + 5' return accurate results.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall evaluate arithmetic expressions with proper operator precedence, ensuring that expressions like '100 - 10% + 5' return accurate results.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 7 of 23 — functional, Must priority

**Implement:** The calculator shall handle rounding using decimal arithmetic to avoid floating-point inaccuracies.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall handle rounding using decimal arithmetic to avoid floating-point inaccuracies.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 8 of 23 — functional, Must priority

**Implement:** The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide clear error messages for malformed expressions, preventing crashes and ensuring user understanding.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 9 of 23 — functional, Must priority

**Implement:** The calculator shall maintain a local SQLite database to store the last 10 calculations, allowing users to access their calculation history.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall maintain a local SQLite database to store the last 10 calculations, allowing users to access their calculation history.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 10 of 23 — functional, Must priority

**Implement:** The calculator shall run locally on each analyst's laptop without requiring network access or external services.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall run locally on each analyst's laptop without requiring network access or external services.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 11 of 23 — functional, Must priority

**Implement:** The calculator shall allow users to input arithmetic expressions directly into the terminal interface.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall allow users to input arithmetic expressions directly into the terminal interface.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 12 of 23 — functional, Must priority

**Implement:** The calculator shall accurately evaluate division operations, including handling division by zero gracefully.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall accurately evaluate division operations, including handling division by zero gracefully.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 13 of 23 — functional, Should priority

**Implement:** The calculator shall provide built-in help documentation accessible from the terminal.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide built-in help documentation accessible from the terminal.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 14 of 23 — functional, Should priority

**Implement:** The calculator shall provide a mechanism for users to view their calculation history from the SQLite database.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide a mechanism for users to view their calculation history from the SQLite database.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 15 of 23 — functional, Could priority

**Implement:** The calculator shall provide a mechanism for users to delete their calculation history from the SQLite database.

**Acceptance criteria (all must pass before this is done):**
- Given valid input, when the function described by this requirement is used, then the system does what it states: The calculator shall provide a mechanism for users to delete their calculation history from the SQLite database.
- Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### Requirement 16 of 23 — nonfunctional, Must priority

**Implement:** The calculator shall evaluate arithmetic expressions quickly enough for interactive use on an analyst's laptop.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall achieve a p99 latency of under 200 milliseconds for evaluating arithmetic expressions.

### Requirement 17 of 23 — nonfunctional, Must priority

**Implement:** The calculator shall be available to analysts whenever they work, because it runs locally on their laptop and needs no network or external service.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall ensure 99.9% availability, allowing analysts to perform calculations at any time during their working hours.

### Requirement 18 of 23 — nonfunctional, Must priority

**Implement:** The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall use decimal arithmetic for all calculations to ensure accuracy in financial computations.

### Requirement 19 of 23 — nonfunctional, Must priority

**Implement:** The calculator shall ensure data retention by maintaining the last 10 calculations in the SQLite database.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall ensure data retention by maintaining the last 10 calculations in the SQLite database.

### Requirement 20 of 23 — nonfunctional, Must priority

**Implement:** The calculator shall ensure compliance with internal data handling policies, given that no sensitive data is processed.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall ensure compliance with internal data handling policies, given that no sensitive data is processed.

### Requirement 21 of 23 — nonfunctional, Should priority

**Implement:** The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall provide audit logging of all calculations performed, including timestamps and user identifiers, stored in the SQLite database.

### Requirement 22 of 23 — nonfunctional, Should priority

**Implement:** The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall be maintainable with a low operational cost, requiring no more than half an engineer-day per quarter for updates and fixes.

### Requirement 23 of 23 — nonfunctional, Should priority

**Implement:** The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.

**Acceptance criteria (all must pass before this is done):**
- Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The calculator shall ensure that all arithmetic operations are performed with a precision of at least 2 decimal places.

## 7. Handoff Guidance

- Use this artifact as implementation input only after acceptance criteria and architecture drivers are reviewed.
- Regenerate when requirements, ADRs, or technology decisions change.
