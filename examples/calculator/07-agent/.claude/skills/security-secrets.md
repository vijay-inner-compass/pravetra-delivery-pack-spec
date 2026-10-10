# Security & Secrets

> Canonical policy version: blueprint-v2-tasks-26-e1ec194e
> Generated: 2026-10-09 10:18:38Z
> Project: E01-calculator
Template — Governed by AIGuard security policy: securityAccess: There is no authentication or authorization model because the tool runs locally under the analyst's own operating-system login and makes no network calls and holds no credentials. Input is parsed by a strict recursive-descent grammar with no eval or scripting, and the history database is created in the user's own profile folder with the user's normal file permissions and holds only expressions and…; securityComplianceAndVendors: There is no authentication or authorization model because the tool runs locally under the analyst's own operating-system login and makes no network calls and holds no credentials. Input is parsed by a strict recursive-descent grammar with no eval or scripting, and the history database is created in the user's own profile folder with the user's normal file permissions and holds only expressions and…; securityDataAndSecrets: There is no authentication or authorization model because the tool runs locally under the analyst's own operating-system login and makes no network calls and holds no credentials. Input is parsed by a strict recursive-descent grammar with no eval or scripting, and the history database is created in the user's own profile folder with the user's normal file permissions and holds only expressions and….

Never hard-code a secret or environment-specific configuration value.
