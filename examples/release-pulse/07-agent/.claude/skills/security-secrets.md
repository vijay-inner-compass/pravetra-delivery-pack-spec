# Security & Secrets

> Canonical policy version: blueprint-v3-tasks-29-4d68dc68
> Generated: 2026-10-09 10:53:27Z
> Project: E02-release-pulse
Template — Governed by AIGuard security policy: securityAccess: Users sign in with the company single sign-on (OpenID Connect through ASP.NET Core authentication) and get team-scoped role-based access with least privilege, and each webhook source is authenticated with its own shared secret that is rotated quarterly and rejected otherwise. All traffic uses TLS 1.3, the database file sits on an encrypted disk volume, and secrets live in the server's protected co…; securityComplianceAndVendors: Users sign in with the company single sign-on (OpenID Connect through ASP.NET Core authentication) and get team-scoped role-based access with least privilege, and each webhook source is authenticated with its own shared secret that is rotated quarterly and rejected otherwise. All traffic uses TLS 1.3, the database file sits on an encrypted disk volume, and secrets live in the server's protected co…; securityDataAndSecrets: Users sign in with the company single sign-on (OpenID Connect through ASP.NET Core authentication) and get team-scoped role-based access with least privilege, and each webhook source is authenticated with its own shared secret that is rotated quarterly and rejected otherwise. All traffic uses TLS 1.3, the database file sits on an encrypted disk volume, and secrets live in the server's protected co….

Never hard-code a secret or environment-specific configuration value.
