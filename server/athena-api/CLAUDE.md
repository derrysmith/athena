# CLAUDE.md — Athena API

Project-specific instructions for the Athena API service. Read the root `AGENTS.md` and `CLAUDE.md` first.

## Solution

`Athena.Api.slnx` — build and test from this directory:

```sh
dotnet build Athena.Api.slnx
dotnet test Athena.Api.slnx
```

## Project Structure

```
server/athena-api/
├── src/
│   ├── Athena.Api.Host/                  # ASP.NET Core Web API (entry point)
│   ├── Athena.Api.Core.Application/      # Application layer (use cases, services, DTOs)
│   ├── Athena.Api.Core.Domain/           # Domain layer (entities, value objects, interfaces)
│   ├── Athena.Api.Infrastructure/        # Infrastructure (external integrations)
│   ├── Athena.Api.Infrastructure.Data/   # Data access (EF Core DbContext, repositories, migrations)
│   ├── Athena.Api.Worker.Database/       # Worker for database migrations
│   └── Athena.Api.Worker.Services/       # Worker for background services, message consumers, cron jobs
├── test/
│   ├── Athena.Tests.Api.Host/
│   ├── Athena.Tests.Api.Core.Application/
│   ├── Athena.Tests.Api.Core.Domain/
│   ├── Athena.Tests.Api.Infrastructure/
│   ├── Athena.Tests.Api.Infrastructure.Data/
│   ├── Athena.Tests.Api.Worker.Database/
│   └── Athena.Tests.Api.Worker.Services/
└── Athena.Api.slnx
```

## Dependency Direction

Domain ← Application ← Infrastructure/Infrastructure.Data ← Host/Workers

- **Domain** has no project references (pure domain model).
- **Application** references Domain only.
- **Infrastructure** and **Infrastructure.Data** reference Application and Domain.
- **Host** and **Workers** reference all layers and wire up DI.
- Test projects reference their corresponding src project.
