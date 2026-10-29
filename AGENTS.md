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

## UI, site and app builds: gate protocol

Applies when the user asks for a new website, landing page, 3D or motion-heavy UI, or a new app. For small edits, fixes and questions do not run this workflow: make the minimal change (diff-guard) and stop.

Precedence: these rules win over any other rule or plugin that says to decompose, dispatch sub-agents or start building immediately. Before Gate 0 is approved, do not dispatch sub-agents and do not write project files other than BRIEF.md and DECISIONS.md.

Modes:
- collab (default): stop at every gate below.
- autopilot: only when the user's message contains the exact word "autopilot". Record assumptions in DECISIONS.md and run Gate 6 only. Never infer autopilot from a detailed prompt, a long task, or the user being away.

What "stop" means: your entire reply at a gate is what you made (the preview path), your questions, and nothing else. If you have a tool that pauses and asks the user, use it. Otherwise ask in chat. Make no further tool calls in that turn. Continue only after the user answers. Record current_gate and gate_status (pending_user or approved) at the top of DECISIONS.md.

| Gate | Name | Before it, you may | You ask | To continue |
| 0 | Intake | read the request, inspect assets/, write BRIEF.md and DECISIONS.md | assets, references, amount of 3D | user answers |
| 1 | Direction | build previews/direction.html | pick or mix of 3 directions | user picks |
| 2 | Type and color | build previews/type-color.html | type pairing, palette tweaks | user picks |
| 3 | Motion and story | build previews/motion.html and STORYBOARD.md | motion personality, scenes | user approves |
| 4 | Hero | build the hero only | does the look match | user approves |
| 5 | Sections | build 2 to 3 scenes per pass | feedback per section | user approves each pass |
| 6 | Final | run visual-qa and the rubric | last changes | user confirms |

Skill order: prompt-optimizer (functional BRIEF only), client-collab (runs the gates), asset-intake, reference-teardown (if references exist), design-taste, storyboard, motion-craft, scene-3d, visual-qa, reviewer.

Always: read DECISIONS.md before every step and never re-ask a recorded answer. Use the client's photos and models for the product and never substitute a generated shape when assets exist. Never report UI work done without screenshots or frames you have looked at. Sub-agents may be used only after Gate 3 is approved, for independent files, never for decisions that belong to a gate.

