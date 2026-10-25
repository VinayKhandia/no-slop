# no-slop: Universal Agent Directive

You are operating under the no-slop protocol: minimal token overhead, zero unnecessary churn, strict diffs, and structured modular execution.

## Execution Workflow

Follow this fixed sequence for all non-trivial tasks:

1. **prompt-optimizer writes BRIEF.md (skip for quick mode)** (`skills/prompt-optimizer/SKILL.md`)
   - prompt-optimizer writes BRIEF.md (skip for quick mode).
   - List explicit assumptions.
   - Ask at most 3 blocking questions; proceed immediately if unblocked.

2. **Planning** (`skills/planner/SKILL.md`)
   - Decompose work into discrete chunks.
   - Initialize and maintain `TASKS.md` with: ID, chunk, role, status, notes.

3. **Design Direction (UI tasks only)** (`skills/design-taste/SKILL.md`)
   - Define concept, palette, typography, spacing, and motion before writing code.
   - Emit `DESIGN.md`. Non-UI tasks skip this stage.

4. **Orchestration & Worker Execution** (`skills/orchestrator/SKILL.md`)
   - Dispatch chunks to roles (`roles/frontend.md`, `roles/backend.md`, `roles/database.md`, `roles/api.md`, `roles/flex.md`).
   - If subagents are supported: run up to 5 parallel workers.
   - If subagents are not supported: execute assigned roles sequentially in this single agent session.
   - Feed each worker only its assigned chunk and relevant files. Never dump the whole repository into context.
   - Serialize work on shared files to avoid merge conflicts.

5. **Diff Guard (applied to EVERY edit)** (`skills/diff-guard/SKILL.md`)
   - Touch only necessary lines.
   - Never reprint full files for localized edits.
   - Block unsolicited refactors, unrequested features, and boilerplate comments.
   - Validate diff size against task scope; revert surplus changes before proceeding.

6. **Review Loop** (`skills/reviewer/SKILL.md`)
   - Act as a senior engineer auditing correctness, security, readability, error handling, and tests.
   - Return a numbered issue list.
   - Have the active role fix issues, re-review, and repeat until clean (max 3 review iterations).
   - Flag any unresolved items if max loops are reached.

7. **Teach Mode Note** (`skills/teach-mode/SKILL.md`)
   - After each completed chunk, append a structured learning note to `LEARNING.md`.
   - Default mode is "on" (keep notes under 120 words).

## Operating Rules

- Keep context lean: read only target files, never load unreferenced files.
- Keep output concise: avoid conversational padding and narrative fluff.
- Respect role boundaries: never edit files assigned to other roles out of turn.
- Update `TASKS.md` state immediately after each chunk completes.

For UI tasks: prompt-optimizer (BRIEF.md) -> reference-teardown if the user gave references (REFERENCES.md) -> design-taste -> storyboard (STORYBOARD.md) -> motion-craft -> scene-3d (read patterns/scroll-world-core.md first) -> build -> visual-qa with Motion QA, rubric and up to 2 Wow Passes -> reviewer. Never report UI work done without looking at frames from a real scroll run.