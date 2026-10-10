# Recommendation Document

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


## 1. Executive Summary

| Metric | Value |
| --- | --- |
| Recommended concept | traditional_software |
| Software required | Yes |
| AI required | No |
| Approval status | Approved |
| Confidence | High |

## 2. Rationale

The proposed solution of a command-line calculator is categorized as 'traditional_software' because it directly addresses the arithmetic errors in invoice totals through deterministic logic. While a 'rules_engine' could also enforce arithmetic rules, it would not provide the same level of user control and simplicity that a dedicated calculator offers. The complexity of implementing a rules engine for this specific use case, where the primary need is accurate arithmetic evaluation, does not justify its use. The traditional software approach ensures that the team can input calculations directly and receive immediate feedback, which is essential for their daily operations.

## 3. Expected Business Value

The solution is expected to reduce rework time from 30 minutes per incorrect total to near zero, saving approximately 6 engineer-hours a week across the team, which translates to about 300 hours a year. This is based on the current error rate of 5% leading to significant rework.

## 4. Data Requirements

The calculator will require input in the form of arithmetic expressions entered via the terminal. Outputs will be the evaluated results of these expressions. The local SQLite database will store the last 10 calculations, requiring a simple schema with fields for expression, result, and timestamp. Latency should be near real-time, with minimal delay for calculations.

## 5. Constraints

The solution must run locally on each analyst's laptop without requiring network access or external services. It must also comply with the team's existing workflow, which relies on terminal usage.

## 6. Assumptions

It is assumed that the finance operations team will consistently use the calculator for all invoice total checks and that they will not revert to manual methods. It is also assumed that the tool will be maintained with updates as needed, without significant changes to its core functionality.

## 7. Evidence Reference

The recommendation is supported by the business problem description, which highlights the need for a reliable calculator to reduce errors and rework time. The proposed solution's feasibility and expected benefits are detailed in the project data.

## 8. Alternative Concepts

- rules_engine

## 9. Hybrid Components

_None captured._

## 10. Major Risks

- Floating-point rounding could produce incorrect results if not handled with decimal arithmetic.
- Malformed expressions could crash the tool instead of providing a clear error message.
- The local history database could become corrupted or edited manually, leading to inaccurate records.

## 11. Review Guidance

- Confirm recommendation alignment with business objectives before approval.
- Validate data, risk, and cost assumptions before delivery planning.
