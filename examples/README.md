# Delivery Pack Specification Examples

**Specification Version**: `1.1.0` (Draft)

This directory contains reference delivery pack examples illustrating the specification profiles:

## 1. Available Examples
Each example is a complete pack whose `integrity.hash` is true; `DeliveryPackValidator` (the Conductor's `validate` command) accepts all three.
- **`minimal/`** (`DeliveryPack.Core`): the minimum viable architectural handoff: manifest, baseline pin, context summary, requirements and architecture summary.
- **`standard/`** (`DeliveryPack.Execution`): two dependent task packets (`TASK-001.json`, `TASK-002.json`), `execution-state.json`, the agent briefing and a policy file.
- **`governed/`** (`DeliveryPack.Governance`): the standard pack plus an implementation readiness report, `05-quality/` and `06-ops/`.

## 2. Real generated packs

These are complete packs produced by the Pravetra platform from a real requirements-to-gate run, not hand-written. They show what a pack looks like at realistic size: primary tasks with sub-tasks (`TASK-NNN.N`), gate reports, a domain data model and the agent policy files. Each validates against `schemas/v1/` and has a true `integrity.hash`.
- **`calculator/`**: an invoice-total calculator (a .NET console application).
- **`release-pulse/`**: a web application (an ASP.NET Core API with background services and a web client).
- **`focus-ledger/`**: a desktop application (.NET with an encrypted local database).

Differences from the platform's own export, so that the packs are safe to publish: the optional `08-commercial/` folder and the PDF copies of the Markdown documents were removed (and their entries dropped from `manifest.json`), the approver's e-mail address was replaced by `approver@example.com`, and `integrity.hash` was recomputed. The technology in each pack (.NET and so on) is that example's own choice; the specification does not require it.

Do not edit a file inside an example without recomputing `integrity.hash` (SPECIFICATION.md section 3.1).
