# Delivery Pack Specification Examples

**Specification Version**: `1.1.0` (Draft)

This directory contains reference delivery pack examples illustrating the specification profiles:

## 1. Available Examples
Each example is a complete pack whose `integrity.hash` is true; `DeliveryPackValidator` (the Conductor's `validate` command) accepts all three.
- **`minimal/`** (`DeliveryPack.Core`): the minimum viable architectural handoff: manifest, baseline pin, context summary, requirements and architecture summary.
- **`standard/`** (`DeliveryPack.Execution`): two dependent task packets (`TASK-001.json`, `TASK-002.json`), `execution-state.json`, the agent briefing and a policy file.
- **`governed/`** (`DeliveryPack.Governance`): the standard pack plus an implementation readiness report, `05-quality/` and `06-ops/`.

Do not edit a file inside an example without recomputing `integrity.hash` (SPECIFICATION.md section 3.1).
