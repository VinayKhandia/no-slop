# Codex Setup Adapter

Integrate the `no-slop` workflow into OpenAI Codex environments, ChatGPT Advanced Data Analysis / Canvas, or API-driven Codex agents.

## 1. Installation Locations

### Project Repository Root
Copy the files directly into your repository:
```bash
cp /path/to/no-slop/AGENTS.md ./AGENTS.md
cp -r /path/to/no-slop/skills ./skills
cp -r /path/to/no-slop/roles ./roles
```

### System / Custom Instructions
If using OpenAI Custom GPTs, API assistant instructions, or workspace system prompts, inject the contents of `AGENTS.md` directly into the system instructions field:
```text
You are governed by the no-slop protocol. Refer to AGENTS.md, skills/, and roles/ in the project root. Perform prompt optimization, maintain TASKS.md, apply surgical diff-guard rules, audit via reviewer loop, and log lessons to LEARNING.md.
```

## 2. Referencing AGENTS.md

At the start of a coding session or in an agent prompt template, state:

```text
Initialize task under AGENTS.md. Load skills/prompt-optimizer/SKILL.md and skills/planner/SKILL.md, generate TASKS.md, and proceed sequentially.
```

## 3. Concurrency Behavior

OpenAI Codex interfaces typically operate sequentially. The orchestrator runs in single-agent fallback mode:
- Assumes the assigned role persona for the active chunk.
- Passes only the required files and role instructions into the immediate context.
- Verifies edits against `diff-guard` before closing the turn.
- Logs a 120-word note to `LEARNING.md` via `teach-mode`.
