# Pravetra Universal Delivery Pack Specification: Security Model

**Specification Version**: `1.0.0` (Draft)  
**Security Disclosure**: `contact@yuktelos.com` | Target Advisory: [Private Vulnerability Reporting](https://github.com/vijay-inner-compass/pravetra-delivery-pack-spec/security/advisories)

---

## 1. Core Security Principle

> **"A Delivery Pack must be treated as untrusted input unless its cryptographic provenance and integrity have been independently established."**

Because a Delivery Pack orchestrates software compilation, test execution, file modifications, and autonomous agent invocations, conforming generators and execution engines must enforce rigorous security boundaries.

This document defines the normative security expectations for all specification conformers.

---

## 2. Threat Model & Key Mitigations

| Threat | Description | Conformance Requirement / Mitigation |
|---|---|---|
| **Path Traversal Attack** | Malicious relative paths (e.g., `../../etc/passwd` or `..\..\Windows\System32`) in task scope or filenames. | **Mandatory Canonicalization**: Consumers MUST resolve absolute paths using filesystem canonicalization (resolving to an absolute path with symlinks and `.`/`..` segments removed) and reject any path escaping the project workspace root. |
| **Arbitrary Shell Injection** | Command payloads containing shell metacharacters (`|`, `;`, `&&`, `` ` ``, `$()`). | **No Shell Interpolation**: All execution commands MUST be defined as an executable filename plus an argument array (`ArgumentList`). Invocation through shell interpreters (`cmd.exe /c`, `sh -c`) is strictly prohibited. |
| **Credential & Secret Leakage** | Hard-coded API keys, tokens, passwords, or certificates stored in task packets or baseline files. | **Secret Prohibition**: Delivery Packs MUST NOT contain plaintext credentials. All outbound toolchains MUST employ automated secret masking in logs and process streams. |
| **Commercial Data Disclosure** | Unsanctioned exposure or modification of sensitive business data, pricing, or proprietary roadmaps. | **Commercial Boundary Isolation**: If `08-commercial/` is present, it MUST be declared restricted. Autonomous coding agents are prohibited from reading, modifying, or publishing its contents. |
| **Supply Chain Tampering** | Modification of task instructions or test assertions after architectural sign-off. | **Cryptographic Verification**: Top-level manifest envelopes MUST include SHA-256 integrity hashes of all referenced artifacts. Engines MUST verify hashes before task execution. |
| **Unbounded Autonomous Action** | Coding agents executing destructive actions (e.g. deleting repositories, pushing to production, overwriting main branch). | **Human Approval Gates**: Destructive operations MUST declare `humanApprovalRequired: true` and halt execution until explicit human confirmation is received. |

---

## 3. Workstation & Process Isolation

Conforming execution engines (such as `pravetra-conductor`) SHOULD execute tasks within isolated execution boundaries:
1. **Isolated Worktree Execution**: Agents work inside isolated git worktrees (e.g., `.worktrees/TASK-001/`) rather than the primary developer checkout until verified.
2. **Local Loopback Only**: Any local management UI or control service MUST bind strictly to IPv4 `127.0.0.1` and IPv6 `::1`, with per-session authentication tokens and strict `Origin` header validation to prevent DNS rebinding attacks.
3. **Pluggable Sandboxing**: Advanced execution profiles MAY dispatch commands into containerized environments (Docker, Dev Containers, or temporary CI virtual machines).

---

## 4. Vulnerability Disclosure & Reporting

If you identify a security vulnerability in the Universal Delivery Pack Specification, schemas, or reference implementations:
1. **Do not disclose publicly via GitHub issues.**
2. Report privately via [GitHub Private Vulnerability Reporting](https://github.com/vijay-inner-compass/pravetra-delivery-pack-spec/security/advisories).
3. Alternatively, email `contact@yuktelos.com` with full technical details, reproduction steps, and potential impact.
4. Security advisories and patches are coordinated under a standard 90-day responsible disclosure timeline.
