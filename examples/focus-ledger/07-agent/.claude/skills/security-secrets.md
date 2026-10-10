# Security & Secrets

> Canonical policy version: blueprint-v2-tasks-23-15bea665
> Generated: 2026-10-09 11:48:57Z
> Project: E03-focus-ledger
Template — Governed by AIGuard security policy: securityAccess: There are no accounts: the user is the owner of the machine and the operating system login is the only identity, and no other process is granted access to the database key held in the secure store. Data is encrypted at rest with AES-256, never leaves the machine (the update check carries no user data, and installers and updates are code-signed), and there are no secrets to manage on a server. Clie…; securityComplianceAndVendors: There are no accounts: the user is the owner of the machine and the operating system login is the only identity, and no other process is granted access to the database key held in the secure store. Data is encrypted at rest with AES-256, never leaves the machine (the update check carries no user data, and installers and updates are code-signed), and there are no secrets to manage on a server. Clie…; securityDataAndSecrets: There are no accounts: the user is the owner of the machine and the operating system login is the only identity, and no other process is granted access to the database key held in the secure store. Data is encrypted at rest with AES-256, never leaves the machine (the update check carries no user data, and installers and updates are code-signed), and there are no secrets to manage on a server. Clie….

Never hard-code a secret or environment-specific configuration value.
