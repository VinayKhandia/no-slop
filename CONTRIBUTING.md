# Contributing to no-slop

Thank you for helping keep AI-assisted software development structured, token-efficient, and slop-free.

## Philosophy

`no-slop` is an open-source, markdown-only framework. We operate under three non-negotiable principles:

1. **Zero Runtime Dependencies**: No Node.js scripts, no Python daemons, no custom MCP servers. All logic is expressed through deterministic markdown instructions that any AI agent can understand and follow.
2. **Strict Token Frugality**: Every word and header added consumes context window tokens. Keep instructions crisp, direct, and under specified line limits.
3. **Teach the Human**: AI coding shouldn't be a black-box code generator; it should level up the human engineer pairing with it.

## Contribution Guidelines

### 1. Skill Guidelines (`skills/<name>/SKILL.md`)
- Every skill must have valid YAML frontmatter containing `name` and `description`.
- Keep the entire body of each skill under 150 lines.
- **NO EMOJIS** anywhere in skill files. Emojis waste context tokens and can degrade prompt steerability across smaller LLMs.
- Skills must be self-contained and support sequential execution if the user's tool does not support multi-agent concurrency.

### 2. Role Guidelines (`roles/<name>.md`)
- Roles must clearly define responsibilities, conventions, and strictly what **NOT** to touch.
- Prevent scope creep between frontend, backend, database, api, and flex specialists.

### 3. Agent Entry Point (`AGENTS.md`)
- Must remain under 120 lines.
- Defines the canonical workflow:
  `prompt-optimizer` -> `planner` -> (`design-taste` if UI) -> `orchestrator` -> `diff-guard` on every edit -> `reviewer` loop -> `teach-mode` note per chunk.

### 4. Adapter Guidelines (`adapters/<tool>.md`)
- Provide exact, tested file paths and configuration commands for the target AI coding tool.
- Include instructions on how the tool references `AGENTS.md` and how it handles concurrency or single-agent fallbacks.

## Pull Request Checklist

Before submitting a PR:
- [ ] No emojis in `skills/` or `AGENTS.md`.
- [ ] Frontmatter in `skills/*/SKILL.md` is valid YAML.
- [ ] All skills are under 150 lines.
- [ ] `AGENTS.md` is under 120 lines.
- [ ] Relative links in `README.md` and documentation resolve properly.
- [ ] Tested in at least one supported AI environment (Claude, Codex, Antigravity, or Cursor).
