# Pravetra Universal Delivery Pack Specification

**Specification Version**: `1.1.0` (Draft)  
**License**: Apache-2.0 (see [LICENSE](LICENSE))  
**Status**: Draft v1.1  
**Canonical Repository**: [https://github.com/vijay-inner-compass/pravetra-delivery-pack-spec](https://github.com/vijay-inner-compass/pravetra-delivery-pack-spec)  

> **Review status.** This is a draft. It has been reviewed only by its maintainer. It has **not** had an independent legal review or an independent security review, and nothing here is legal advice or a security certification. Conformance claims should not depend on this review. Independent review comments are welcome (see [CONTRIBUTING.md](CONTRIBUTING.md) and, for security issues, [SECURITY.md](SECURITY.md)).

---

## 1. Overview & Purpose

The **Pravetra Universal Delivery Pack Specification** is an open, vendor-neutral standard for governing software-delivery handoffs between architecture/governance systems, autonomous coding agents, CI/CD pipelines, and human approval workflows.

Modern autonomous coding agents (from any vendor, and custom orchestrators) are frequently constrained by ambiguous prompt context or unbounded repository access. A Delivery Pack provides an unambiguous, version-pinned, tamper-evident contract between software architects and autonomous execution engines.

Tagline: *"Intelligence from idea to outcome."*

---

## 2. Positioning & Intellectual Property Boundary

> **Pravetra Universal Delivery Pack Specification**  
> **Pravetra Conductor — Proprietary reference implementation of the Pravetra Universal Delivery Pack Specification**

### Important Clarifications
1. **A Vendor-Neutral Specification, Not an Open-Source Conductor**: This specification is vendor-neutral and open. Implementers are free to build independent, compatible execution engines, CI runners, and generator tools subject to the applicable specification license and trademark policy.
2. **Proprietary Reference Implementation**: **Pravetra Conductor** (`pconductor`) is a closed-source proprietary desktop orchestrator developed by Yuktelos. Conductor is not open source and its implementation code is not part of this specification repository.
3. **No Lock-in**: Compliance with this specification does not require Pravetra Conductor, the Pravetra cloud platform, or any single AI model vendor.

---

## 3. Specification Suite

The specification suite consists of:

- **[SPECIFICATION.md](SPECIFICATION.md)**: The normative protocol standard detailing the 8 delivery pack sections, manifest envelope, atomic task packet contract, and execution state machine.
- **[CONFORMANCE.md](CONFORMANCE.md)**: Conformance profiles (`DeliveryPack.Core`, `DeliveryPack.Execution`, `DeliveryPack.Governance`, `DeliveryPack.Full`) and self-certification verification criteria.
- **[VERSIONING.md](VERSIONING.md)**: Semantic versioning rules, forward/backward compatibility, and schema evolution policies.
- **[EXTENSIONS.md](EXTENSIONS.md)**: Namespace-isolated extension guidelines for vendor adapters (non-normative).
- **[SECURITY.md](SECURITY.md)**: Specification-level security model, path traversal boundaries, credential redaction, and untrusted pack handling.
- **[CONTRIBUTING.md](CONTRIBUTING.md)**: How to propose improvements and participate in the specification RFC process.
- **[TRADEMARKS.md](TRADEMARKS.md)**: Trademark usage guidelines for "Pravetra" and "Pravetra Delivery Pack".
- **[CHANGELOG.md](CHANGELOG.md)**: Release and version history.
- **[JSON Schemas v1](schemas/v1/)**: Formal Draft 2020-12 JSON Schemas for manifest, task packets, execution state, policies, and artifacts.
- **[Reference Examples](examples/)**: Synthetic `minimal`, `standard`, and `governed` sample delivery packs.
- **[Conformance Test Vectors](conformance/)**: Valid and intentionally invalid packs for test verification.

---

## 4. Conceptual Architecture

```text
                 PRODUCERS
        ┌────────────────────────┐
        │ Pravetra Platform      │
        │ Third-party tools      │
        │ Human-authored tooling │
        └────────────┬───────────┘
                     │
                     ▼
        ┌────────────────────────┐
        │  UNIVERSAL DELIVERY    │
        │   PACK SPECIFICATION   │
        └────────────┬───────────┘
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
      Pravetra     CI/CD      Third-party
     Conductor    consumer    implementation
    (proprietary)
```

---

## 5. Quick Start for Implementers

### Consuming a Delivery Pack
A compliant execution engine:
1. Validates `00-manifest/manifest.json` against [`schemas/v1/delivery-pack-manifest.schema.json`](schemas/v1/delivery-pack-manifest.schema.json).
2. Reads the pinned baseline in `01-baseline/baseline-pin.md`.
3. Processes atomic task packets in `04-delivery/` sequentially or in parallel according to `dependsOn` and `parallelSafe`.
4. Executes declared compilation and test commands using argument-array execution (no shell involved) rather than shell string interpolation.
5. Updates runtime progress in `07-agent/execution-state.json`.

---

## 6. Feedback & Governance

Questions and proposals regarding the specification may be submitted via GitHub Issues and Pull Requests on the official specification repository.
