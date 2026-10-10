# Contributing to the Pravetra Universal Delivery Pack Specification

Thank you for your interest in improving the **Pravetra Universal Delivery Pack Specification**!

This repository hosts the open, vendor-neutral specification, JSON Schemas, conformance criteria, and test vectors. Please review these guidelines before submitting proposals, issues, or pull requests.

---

## 1. Scope of Contributions

This repository is dedicated to the **Universal Delivery Pack Specification**:
- Standard prose and normative terminology (`SPECIFICATION.md`)
- Conformance criteria and profiles (`CONFORMANCE.md`)
- Formal JSON Schemas (`schemas/v1/`)
- Extension mechanisms and namespace standards (`EXTENSIONS.md`)
- Synthetic examples and conformance test vectors (`examples/`, `conformance/`)

> **Note on Implementations**:  
> Implementation source code for **Pravetra Conductor** or the **Pravetra Platform** is proprietary and not hosted here. Third-party execution engines, CLI runners, and adapters are encouraged to publish their own open or commercial implementations referencing this standard.

---

## 2. Proposing Changes (RFC Workflow)

### 2.1 Non-Normative Changes (Typos, Clarifications, Test Vectors)
1. Open a GitHub Issue or submit a direct Pull Request.
2. Clearly describe the typo, clarification, or synthetic test case.
3. Verify all schemas and examples pass local validation before submitting.

### 2.2 Normative Changes (Schema Additions, New Capabilities, Protocol Semantics)
For additions to normative schemas or protocol rules:
1. **Open a Discussion / RFC Issue**: Outline the motivation, concrete use case, and proposed schema modification.
2. **Backward Compatibility Impact**: Explain how existing consumers and generators will handle the proposed change under [VERSIONING.md](VERSIONING.md).
3. **Submit PR with Schema & Test Vectors**:
   - Update relevant schema under `schemas/v1/`.
   - Update `SPECIFICATION.md` or `CONFORMANCE.md`.
   - Add matching valid and invalid test vectors in `conformance/`.
   - Update `CHANGELOG.md`.

---

## 3. Developer Certificate of Origin (DCO)

All pull requests must include a Developer Certificate of Origin sign-off line in the commit message:

```text
Signed-off-by: Jane Doe <jane.doe@example.com>
```

By adding this line, you certify that you have the right to submit the contribution under the Apache License, Version 2.0.

---

## 4. IP Cleanliness & Hygiene Rules

Contributors must ensure:
1. **Zero Proprietary Information**: No internal prompts, customer data, proprietary algorithms, production URLs, or internal secrets.
2. **Synthetic Data Only**: All test vectors and examples must use synthetic repositories and fictitious organizations.
3. **Vendor Neutrality**: Proposed changes must not require or endorse any single AI model vendor, IDE, or commercial platform.
