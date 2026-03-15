# CLAUDE.md

This file provides Claude-specific guidance on top of the shared rules in `AGENTS.md`. Claude should read both files; `AGENTS.md` for general project rules, this file for Claude-specific behavior.

## Reading Order

1. Read `AGENTS.md` first — it contains project overview, structure, build commands, and conventions that apply to all agents.
2. Read this file for Claude-specific instructions.
3. If a subdirectory contains its own `CLAUDE.md`, read that too for project-specific overrides.

## Claude-Specific Behavior

### Tool Usage

- Use the Grep and Glob tools to search the codebase — do not shell out to `grep`, `rg`, or `find`.
- Use the Read tool to read files — do not use `cat`, `head`, or `tail`.
- Use the Edit tool for targeted changes — do not use `sed` or `awk`.
- Run build and test commands via the Bash tool.

### Working in the Monorepo

- Before making changes, identify which project(s) under `client/`, `mobile/`, `server/`, or `shared/` are affected.
- Run builds and tests from the specific project directory (e.g., `client/athena-web/`, `server/athena-api/`), not the repo root, unless a root-level script exists for that purpose.
- When a change spans multiple projects (e.g., a shared library and a consuming service), make and verify changes in dependency order: shared → server → client/mobile.

### Code Generation

- **Frontend**: Generate TypeScript. Use `import`/`export` syntax (ESM). Do not use `require()`.
- **Backend**: Generate C# targeting the .NET version specified in each project's `global.json` or `.csproj`. Use file-scoped namespaces and nullable reference types.
- Do not add boilerplate comments like `// TODO: implement` or `// Add your code here`.
- Do not add XML doc comments or JSDoc unless the user asks for documentation.

### Git Workflow

- Do not commit unless explicitly asked.
- Do not push unless explicitly asked.
- Do not amend commits unless explicitly asked.
- When committing, stage only the files relevant to the change — avoid `git add -A`.

### Asking vs. Acting

- If a task is ambiguous or could affect multiple projects, ask for clarification before proceeding.
- If unsure which project a file belongs to, explore the directory structure first.
- For destructive or hard-to-reverse operations, confirm with the user before executing.
