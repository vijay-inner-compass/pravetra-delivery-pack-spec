# Architecture Boundaries

> Canonical policy version: blueprint-v2-tasks-23-15bea665
> Generated: 2026-10-09 11:48:57Z
> Project: E03-focus-ledger
Decomposition: ModularMonolith.

No existing-system constraints — greenfield architecture choice, revisited as real design work narrows scope. Requirements this architecture must satisfy: The application must ensure that the timer updates in real-time with a maximum latency of 1 second. | The application must start and record focus sessions without a network connection, so the timer is available whenever the user's computer is on. | The application must encrypt all stored data at rest using AES-256 encryption to protect sensitive client information. | The application must provide a backup and recovery mechanism that allows users to restore their session data from an encrypted local backup file. | The application must comply with GDPR regulations, allowing users to delete their data upon request. | The application must ensure that session data is backed up at least once a week to prevent data loss.

Do not cross a task's own target scope without an explicit, recorded dependency.
