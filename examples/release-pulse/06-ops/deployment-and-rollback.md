# Deployment, Observability and Rollback

| Concern | Status/Detail |
| --- | --- |
| Deployment & Infrastructure | Complete — 1 deployable unit(s) to provision and deploy independently. Infrastructure: technologyInterfaces: The service runs as one .NET host on a server the platform team already operates on the internal network: an ASP.NET Core API with a web client and three hosted background workers (ingest, scoring, digest), one SQLite database file in write-ahead mode, and a SQLite-backed job table between the API and the workers; there is nothing else to provision. The API exposes versioned REST endpoints documen…; technologyRuntime: The service runs as one .NET host on a server the platform team already operates on the internal network: an ASP.NET Core API with a web client and three hosted background workers (ingest, scoring, digest), one SQLite database file in write-ahead mode, and a SQLite-backed job table between the API and the workers; there is nothing else to provision. The API exposes versioned REST endpoints documen…. |
| Observability | Template — Structured logging, request/error metrics, and distributed tracing across every deployable unit and external integration. |
| Migration | NotApplicable — Greenfield project — no legacy system or data to migrate. |

Rollback: every task packet lists its own rollback steps (`rollback`) — this document is the solution-wide summary.
