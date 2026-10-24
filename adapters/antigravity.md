# Antigravity Setup Adapter

Integrate the `no-slop` workflow into Google Antigravity (AGY CLI and Antigravity IDE).

## 1. Installation Locations

### Project-Specific Installation
Copy `no-slop` files into your active Antigravity workspace:
```bash
cp /path/to/no-slop/AGENTS.md ./AGENTS.md
cp -r /path/to/no-slop/skills ./.gemini/antigravity/skills
cp -r /path/to/no-slop/roles ./.gemini/antigravity/roles
```
Antigravity automatically loads rule directives from `AGENTS.md` and discovers all skills declared inside `.gemini/antigravity/skills/` or `.agent/skills/`.

### Global User-Level Installation
To enable `no-slop` across all Antigravity projects:
```bash
mkdir -p ~/.gemini/antigravity/skills
cp -r /path/to/no-slop/skills/* ~/.gemini/antigravity/skills/
mkdir -p ~/.gemini/antigravity/roles
cp -r /path/to/no-slop/roles/* ~/.gemini/antigravity/roles/
mkdir -p ~/.gemini/config/rules
cp /path/to/no-slop/AGENTS.md ~/.gemini/config/rules/no-slop.md
```

## 2. Referencing AGENTS.md

Antigravity auto-discovers `AGENTS.md` at the project root or in rule directories. You can also explicitly trigger it:

```text
Follow AGENTS.md workflow. Optimize prompt, create TASKS.md, establish DESIGN.md if building UI, and orchestrate workers.
```

## 3. Concurrency Behavior

Antigravity natively supports background subagents via `invoke_subagent`. The orchestrator will:
- Check `CONFIG.max_parallel_workers` (default: 5).
- Dispatch independent chunks concurrently across specialized subagents.
- Pass only assigned chunks and relevant file paths to subagents.
- Serialize chunks that share target files to avoid merge conflicts.
- Audit work with `reviewer` loops and append educational logs to `LEARNING.md`.
