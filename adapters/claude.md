# Claude Setup Adapter

Integrate the `no-slop` workflow into Claude (Claude Projects, Claude Code CLI, or Claude Web).

## 1. Installation Locations

### Claude Projects (Web)
1. In your Claude Project, go to the **Project Knowledge** pane.
2. Upload the `no-slop` directory or the following core files:
   - `AGENTS.md`
   - `skills/` directory (all `SKILL.md` files)
   - `roles/` directory (all role `.md` files)
3. In **Custom Instructions**, add:
   ```text
   Follow the instructions in AGENTS.md for all coding and refactoring tasks. Adhere strictly to the no-slop protocol, skills, and role constraints.
   ```

### Claude Code (CLI)
1. Place `no-slop` in your project root or in a `.claude/` configuration folder:
   ```bash
   cp -r /path/to/no-slop/skills ./skills
   cp -r /path/to/no-slop/roles ./roles
   cp /path/to/no-slop/AGENTS.md ./CLAUDE.md
   ```
2. Claude Code automatically reads `CLAUDE.md` on startup.

## 2. Referencing AGENTS.md

When initiating a coding request in Claude, reference the workflow:

```text
Follow AGENTS.md. Optimize prompt, create TASKS.md, establish DESIGN.md if UI is required, and run sequential role execution.
```

## 3. Concurrency Behavior

Claude functions primarily as a single-turn conversational agent or sequential tool runner. The `orchestrator` will automatically fall back to sequential execution:
- Execute `prompt-optimizer` -> `planner` -> (UI: `design-taste`).
- Execute each chunk in `TASKS.md` sequentially.
- Enforce `diff-guard` on all edits.
- Run `reviewer` self-audit.
- Record `teach-mode` entry in `LEARNING.md`.
