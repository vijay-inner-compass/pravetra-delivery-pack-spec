# Requirements & Backlog Specification

This document provides the canonical requirements catalog and agile product backlog for **E03-focus-ledger**. It is structured to support **Scrum** (Product Backlog Items & User Stories with Acceptance Criteria), **Agile** delivery increments, **SAFe** (Capabilities, Enablers, & Non-Functional Requirements), and **Classic SDLC** functional specifications.

## Backlog Summary

| Metric | Count |
| --- | --- |
| Total Requirements / Backlog Items | 21 |
| Functional Stories | 10 |
| Non-Functional Requirements (NFR Enablers) | 9 |
| Business Outcomes & Strategic Capabilities | 2 |
| Approved (Critical-Approved) | 16 |

## Backlog Items & User Stories

| ID | Kind | Priority | Status | Statement / User Story |
| --- | --- | --- | --- | --- |
| 1146a2e75b0f4b86bc397d3679daff5f | functional | Must | Critical-Approved | The application must allow users to export their timesheet as a CSV or PDF file. |
| 465de9a73abe4e8183fb37c08fdae942 | nonfunctional | Must | Critical-Approved | The application must ensure that session data is backed up at least once a week to prevent data loss. |
| 46c54cc0b3cc40558acdaf676d1dc0a4 | functional | Must | Critical-Approved | The application must provide a weekly review screen that totals sessions by client and task type. |
| 628dcd6237e94b23915d06e2ad55092f | functional | Must | Critical-Approved | The application must allow users to view a history of their past focus sessions, including client names, task descriptions, and duration. |
| 696b52d5dc1a4baaa56c2a265f8d8f4a | functional | Must | Critical-Approved | The application must display a timer in the system tray that counts the duration of the focus session. |
| 9c6e7e99970c4390b4a84b428a413210 | functional | Must | Critical-Approved | The application must allow users to manually stop a focus session and record the end time. |
| 9fd91fb5542344b7b96640c91c3183f7 | functional | Must | Critical-Approved | The application must allow users to start a focus session by selecting a client and entering a one-line task description. |
| a52c3c8b61e144108f829621f377371c | nonfunctional | Must | Critical-Approved | The application must provide a backup and recovery mechanism that allows users to restore their session data from an encrypted local backup file. |
| ada5a7f746cb43cbafdbd946362f97f4 | nonfunctional | Must | Critical-Approved | The application must encrypt all stored data at rest using AES-256 encryption to protect sensitive client information. |
| b91ca49987594129b0cc1b0ab9c246fb | business | Must | Critical-Approved | Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant. |
| b99deb3fe3df434aae4c859dddadb728 | business | Must | Critical-Approved | Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes. |
| c027785e929c49dd9471a69a24dadb4b | nonfunctional | Must | Critical-Approved | The application must comply with GDPR regulations, allowing users to delete their data upon request. |
| cd93e399204a416989d0266a648ed2cc | functional | Must | Critical-Approved | The application must prompt the user after 90 minutes of inactivity to confirm whether to continue the session or trim it. |
| d50a717c6a8344a589efbcdbfc3e9a0c | nonfunctional | Must | Critical-Approved | The application must start and record focus sessions without a network connection, so the timer is available whenever the user's computer is on. |
| d9527b35c4494cb2807211133ea4b2f0 | functional | Must | Critical-Approved | The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database. |
| f6c44d6ffbc24c9ea59776bf4c6ba2ce | nonfunctional | Must | Critical-Approved | The application must ensure that the timer updates in real-time with a maximum latency of 1 second. |
| 587516bd457841f7866b8f1079c5599e | functional | Should | draft | The application must provide a mechanism for users to edit or delete past focus sessions. |
| 847d4406d0f94002b149721df290b3f2 | functional | Should | draft | The application must notify users of any unsaved session data when they attempt to close the application. |
| a80fbd1ef94146cb91db0881301a782e | nonfunctional | Should | draft | The application must allow users to access their historical session data for as long as they keep it. |
| e1a2605dde7242deb5b8a06e426b7ad7 | nonfunctional | Should | draft | The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen. |
| e1d429643cc7408d9c005d08f4386f2f | nonfunctional | Should | draft | The application must have a user interface that adheres to accessibility standards, ensuring usability for all users. |

---

## Item Details & Acceptance Criteria

### 1146a2e75b0f4b86bc397d3679daff5f: The application must allow users to export their timesheet as a CSV or PDF file.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to export their timesheet as a CSV or PDF file.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### 465de9a73abe4e8183fb37c08fdae942: The application must ensure that session data is backed up at least once a week to prevent data loss.

- **Kind**: nonfunctional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that session data is backed up at least once a week to prevent data loss.

### 46c54cc0b3cc40558acdaf676d1dc0a4: The application must provide a weekly review screen that totals sessions by client and task type.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must provide a weekly review screen that totals sessions by client and task type.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### 628dcd6237e94b23915d06e2ad55092f: The application must allow users to view a history of their past focus sessions, including client names, task descriptions, and duration.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to view a history of their past focus sessions, including client names, task descriptions, and duration.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### 696b52d5dc1a4baaa56c2a265f8d8f4a: The application must display a timer in the system tray that counts the duration of the focus session.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must display a timer in the system tray that counts the duration of the focus session.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### 9c6e7e99970c4390b4a84b428a413210: The application must allow users to manually stop a focus session and record the end time.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to manually stop a focus session and record the end time.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### 9fd91fb5542344b7b96640c91c3183f7: The application must allow users to start a focus session by selecting a client and entering a one-line task description.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must allow users to start a focus session by selecting a client and entering a one-line task description.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### a52c3c8b61e144108f829621f377371c: The application must provide a backup and recovery mechanism that allows users to restore their session data from an encrypted local backup file.

- **Kind**: nonfunctional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must provide a backup and recovery mechanism that allows users to restore their session data from an encrypted local backup file.

### ada5a7f746cb43cbafdbd946362f97f4: The application must encrypt all stored data at rest using AES-256 encryption to protect sensitive client information.

- **Kind**: nonfunctional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must encrypt all stored data at rest using AES-256 encryption to protect sensitive client information.

### b91ca49987594129b0cc1b0ab9c246fb: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.

- **Kind**: business | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Enable independent consultants and freelance developers to accurately track their billable hours, reducing under-billing by at least 4 hours per week, which translates to approximately $15,000 annually per consultant.

### b99deb3fe3df434aae4c859dddadb728: Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.

- **Kind**: business | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the solution is in use, when the people it is built for carry out the work this requirement describes, then the stated outcome is observed and recorded: Provide users with a trustworthy weekly timesheet that can be generated in under 2 minutes.

### c027785e929c49dd9471a69a24dadb4b: The application must comply with GDPR regulations, allowing users to delete their data upon request.

- **Kind**: nonfunctional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must comply with GDPR regulations, allowing users to delete their data upon request.

### cd93e399204a416989d0266a648ed2cc: The application must prompt the user after 90 minutes of inactivity to confirm whether to continue the session or trim it.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must prompt the user after 90 minutes of inactivity to confirm whether to continue the session or trim it.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### d50a717c6a8344a589efbcdbfc3e9a0c: The application must start and record focus sessions without a network connection, so the timer is available whenever the user's computer is on.

- **Kind**: nonfunctional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must maintain an availability of 99.9% during the pilot phase, ensuring that users can access the timer functionality at all times.

### d9527b35c4494cb2807211133ea4b2f0: The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.

- **Kind**: functional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must store all session data, including client names, task descriptions, start and end times, and user notes, in an encrypted local SQLite database.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### f6c44d6ffbc24c9ea59776bf4c6ba2ce: The application must ensure that the timer updates in real-time with a maximum latency of 1 second.

- **Kind**: nonfunctional | **Priority**: Must | **Status**: Critical-Approved

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that the timer updates in real-time with a maximum latency of 1 second.

### 587516bd457841f7866b8f1079c5599e: The application must provide a mechanism for users to edit or delete past focus sessions.

- **Kind**: functional | **Priority**: Should | **Status**: draft

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must provide a mechanism for users to edit or delete past focus sessions.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### 847d4406d0f94002b149721df290b3f2: The application must notify users of any unsaved session data when they attempt to close the application.

- **Kind**: functional | **Priority**: Should | **Status**: draft

**Acceptance Criteria (Given / When / Then)**:
1. Given valid input, when the function described by this requirement is used, then the system does what it states: The application must notify users of any unsaved session data when they attempt to close the application.
1. Given input that does not meet the conditions the requirement states, when it is submitted, then the system refuses it with a clear explanation and records the refusal in the audit log.

### a80fbd1ef94146cb91db0881301a782e: The application must allow users to access their historical session data for as long as they keep it.

- **Kind**: nonfunctional | **Priority**: Should | **Status**: draft

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must allow for data retention of at least 5 years, enabling users to access historical session data.

### e1a2605dde7242deb5b8a06e426b7ad7: The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.

- **Kind**: nonfunctional | **Priority**: Should | **Status**: draft

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must ensure that the user interface is responsive, with a maximum load time of 2 seconds for any screen.

### e1d429643cc7408d9c005d08f4386f2f: The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.

- **Kind**: nonfunctional | **Priority**: Should | **Status**: draft

**Acceptance Criteria (Given / When / Then)**:
1. Given the system is running under its normal conditions, when the quality target in this requirement is measured, then the result meets it and the measurement is kept as evidence: The application must have a user interface that adheres to accessibility standards, ensuring usability for all users.

