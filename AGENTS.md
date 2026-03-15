# AGENTS.md

This file provides guidance to all AI coding agents (including Claude, Codex, Copilot, etc.) working in this repository.

## Project Overview

**athena** is a monorepo containing client applications, backend services, and shared libraries.

| Layer              | Tech Stack        | Location  |
| ------------------ | ----------------- | --------- |
| Client apps        | Next.js (Node)    | `client/` |
| Mobile Hybrid apps | Expo/React-Native | `mobile/` |
| Backend services   | .NET Core         | `server/` |
| Shared libraries   | Cross-platform    | `shared/` |

## Repository Structure

```
> athena
	> client	# client applications (next.js)
		> athena-web
	> mobile	# mobile applications (expo/react-native)
		> athena-app
	> server	# backend services (.net core)
		> athena-api
	> shared	# shared libraries
		> athena-dotnet
		> athena-nodejs
	- AGENTS.md	# instructions for all AI agents (this file)
	- CLAUDE.md	# intructions specifically for claude
	- README.md
```

## Environment Requirements

| Tool     | Minimum Version |
| -------- | --------------- |
| Bun      | 1.x             |
| .NET SDK | 9.0             |
| Node.js  | 22.x (for Expo) |

## Build & Test Commands

### Frontend / TypeScript (Bun)

Run these from within the relevant app directory under `client/athena-*/` or `mobile/athena-*/`.

```sh
bun install       # Install dependencies
bun run build     # Build
bun run dev       # Dev server
bun run lint      # Lint
bun test          # Test
```

### Backend (.NET Core)

Run these from within the relevant project/solution directory under `server/athena-*/`.

```sh
dotnet restore    # Restore dependencies
dotnet build      # Build
dotnet run        # Run
dotnet test       # Test
dotnet format     # Lint / format
```

## Conventions

### General

- Keep changes scoped to the relevant project within the monorepo.
- Do not introduce cross-project dependencies without discussion.
- Prefer editing existing files over creating new ones.
- One logical change per commit.
- Write clear, concise commit messages.

### Frontend / TypeScript

- Use Bun as the package manager and runtime for all TypeScript apps and libraries. Do not use `npm`, `yarn`, or `pnpm`.
- Use TypeScript for all new code.
- Use Biome for linting and formatting. Do not use ESLint or Prettier.
- Use functional React components with hooks.
- Prefer named exports over default exports.

### Backend (.NET Core)

- Follow standard C# naming conventions (PascalCase for public members, camelCase for locals).
- Use async/await for all I/O-bound operations.
- Keep controllers thin — push logic into services.
- Use dependency injection; do not instantiate services directly.
- Prefer DDD-style architecture and boundaries.
- Always use the `.slnx` solution format. Do not use the legacy `.sln` format.
- Use PostgreSQL as the database and Entity Framework Core as the ORM.
- Use EF Core migrations for schema changes. Do not write raw DDL.

### Shared Libraries

- Shared libraries in `shared/` must not depend on app- or service-specific code.
- Keep library APIs minimal and well-documented.
- Create one library per logical responsibility.
  - For .NET Core libraries, create a new solution for the logical grouping.
  - For Node.js/TypeScript libraries, create a new package for the logical grouping. Use Bun as the package manager.

## Testing

- All new features and bug fixes should include tests.
- Frontend: use the testing framework configured in each app (e.g., Jest, Vitest).
- Backend: always use xUnit test projects.
- Run the relevant test suite before submitting changes.

## Branch Strategy

- `main` is the primary branch and should always be in a clean, deployable state.
- Tags represent versions of the codebase that made it to production.
- All work branches should be created from `main` and kept short-lived.
- Branch names must include the related GitHub issue number: `<type>/<issue>/<short-description>` (e.g., `issues/042/user-auth`, `hotfix/103/-null-ref`).
- Merge back to `main` via pull request.

## Security

- Never commit secrets, credentials, or connection strings.
- Use environment variables or secret managers for sensitive configuration.
- Do not disable SSL/TLS verification or security middleware.
