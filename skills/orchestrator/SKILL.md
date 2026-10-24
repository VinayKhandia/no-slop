---
name: orchestrator
description: Dispatches atomic task chunks to specialized roles with minimal context, managing concurrency and serializing shared file edits.
---

# Orchestrator

Route task chunks from `TASKS.md` to specialized roles. Control concurrency and enforce strict context isolation.

## Configuration

The following parameters govern orchestrator dispatch:

```yaml
CONFIG:
  max_parallel_workers: 5
  subagent_mode: auto  # auto | enabled | disabled
  role_definitions_path: roles/
```

- If the active coding environment supports background subagents or parallel dispatch, spawn up to `max_parallel_workers` concurrently.
- If the environment lacks subagent execution (or is running in a single-turn agent like basic Claude or Cursor chat), fall back automatically to sequential single-agent execution, assuming each role persona in sequence.

## Roles Directory

Every task must map to one of five designated roles:
- `roles/frontend.md`: UI components, styling, client state.
- `roles/backend.md`: Core logic, domain services, compute tasks.
- `roles/database.md`: Schemas, migrations, models, data persistence.
- `roles/api.md`: HTTP/RPC endpoints, route handlers, serialization.
- `roles/flex.md`: Tooling, build scripts, tests, cross-cutting glue.

## Context Boundary Rules

1. **Targeted File Injection**: Never pass the entire project tree or codebase into a worker's context. Pass ONLY:
   - The specific task chunk description from `TASKS.md`.
   - The exact role instruction file (e.g., `roles/backend.md`).
   - The specific file paths directly required to implement or test that chunk.
2. **Prevent Shared File Collisions**:
   - If two or more concurrent chunks touch the same file (e.g., `routes.ts` or `schema.sql`), they must NOT be dispatched in parallel.
   - Enforce sequential execution on all tasks sharing identical target files.
3. **Execution Loop per Chunk**:
   - Step 1: Assign chunk and update `TASKS.md` to `in_progress`.
   - Step 2: Role performs work adhering to `diff-guard`.
   - Step 3: Run `reviewer` loop.
   - Step 4: Run `teach-mode` to append to `LEARNING.md`.
   - Step 5: Mark chunk `done` in `TASKS.md`.
