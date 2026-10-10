# Recommendation Document

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


## 1. Executive Summary

| Metric | Value |
| --- | --- |
| Recommended concept | traditional_software |
| Software required | Yes |
| AI required | No |
| Approval status | Approved |
| Confidence | High |

## 2. Rationale

The proposed solution, a .NET desktop application called Focus Ledger, is best categorized as a traditional software application. It addresses the specific needs of independent consultants and freelancers by providing a reliable, offline timer that tracks billable hours without requiring cloud connectivity. While workflow automation and rules engines could streamline some processes, they do not adequately address the core problem of accurately tracking time in a user-friendly manner. Workflow automation would not capture the necessary offline functionality and real-time tracking, while a rules engine would not provide the intuitive interface needed for users to start and stop timers easily. The deterministic nature of the problem allows for a straightforward software solution without the complexities introduced by AI.

## 3. Expected Business Value

$16,000 per year per user, based on the recovery of 4 billable hours a week at $80 per hour (from the business objectives section).

## 4. Data Requirements

The application will require user input for client names and task descriptions, stored in an encrypted local SQLite database. The expected volume is one user per installation, with data stored in a structured format that includes timestamps for start and stop times, client identifiers, and task types. Latency targets are immediate for user interactions, with data saved locally in real-time.

## 5. Constraints

The application must operate offline, ensuring that all data is stored locally and encrypted. It must also comply with user confidentiality requirements, meaning no data can be transmitted to external servers. The application should be lightweight to run on standard laptops without significant resource consumption.

## 6. Assumptions

Users will be willing to adopt a desktop application that meets their confidentiality needs. The application will effectively reduce the time spent on manual tracking and improve billing accuracy. Users will have the technical capability to install and operate a .NET application on their devices.

## 7. Evidence Reference

The recommendation is supported by the business problem description, which highlights the need for a reliable offline solution that respects client confidentiality, as well as the expected recovery of 4 to 6 billable hours a week per user.

## 8. Alternative Concepts

- workflow_automation
- rules_engine

## 9. Hybrid Components

_None captured._

## 10. Major Risks

- Data loss due to hardware failure or accidental deletion, which could result in loss of tracked hours.
- User resistance to adopting a new tool, especially if they are accustomed to existing manual methods.

## 11. Review Guidance

- Confirm recommendation alignment with business objectives before approval.
- Validate data, risk, and cost assumptions before delivery planning.
