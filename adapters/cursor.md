# Cursor Setup Adapter

Integrate the `no-slop` workflow into Cursor (Cursor IDE, Composer, and Chat).

## 1. Installation Locations

### Project-Specific (.cursor/rules)
Cursor supports directory-based rules inside `.cursor/rules/`:
```bash
mkdir -p .cursor/rules
cp /path/to/no-slop/AGENTS.md .cursor/rules/no-slop.mdc
cp -r /path/to/no-slop/skills ./skills
cp -r /path/to/no-slop/roles ./roles
```
Ensure frontmatter in `.cursor/rules/no-slop.mdc` contains:
```markdown
---
description: Universal no-slop structured development workflow
globs: *
alwaysApply: true
---
```

### Legacy .cursorrules
Alternatively, place `AGENTS.md` content directly in `.cursorrules` in your repository root:
```bash
cp /path/to/no-slop/AGENTS.md ./.cursorrules
cp -r /path/to/no-slop/skills ./skills
cp -r /path/to/no-slop/roles ./roles
```

## 2. Referencing AGENTS.md

In Cursor Composer (`Cmd+I` or `Ctrl+I`) or Chat (`Cmd+L`), reference the workflow:

```text
Follow no-slop rules in AGENTS.md. Optimize prompt, update TASKS.md, use DESIGN.md for UI, apply diff-guard, and log lessons to LEARNING.md.
```

## 3. Concurrency Behavior

Cursor Composer operates sequentially within the open workspace:
- The orchestrator runs in sequential fallback mode.
- Each chunk in `TASKS.md` is applied one by one using surgical diffs.
- `diff-guard` ensures Cursor does not regenerate untouched parts of files.
- Run the `reviewer` checklist before accepting Composer changes.
- Append a concise educational note to `LEARNING.md` via `teach-mode`.
