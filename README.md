# no-slop

**Structured, token-efficient, senior-grade AI software engineering across all major AI coding tools.**

No code runtime. No MCP servers. Pure, high-leverage markdown instruction files.

Works out of the box with **Claude**, **OpenAI Codex**, **Google Antigravity**, and **Cursor**.

---

## The Problem with Default AI Coding

Most AI coding agents produce "slop":
- **Token Inflation**: They ingest entire repositories and reprint 500-line files to change three lines of code.
- **Unrequested Churn**: They rewrite working functions, introduce unwanted dependencies, and add decorative comments.
- **Generic Design**: They generate cookie-cutter Tailwind cards and standard templates with zero aesthetic identity.
- **Black-Box Isolation**: They build silently without explaining why decisions were made, keeping the human developer in the dark.

## The no-slop Philosophy

1. **Surgical Diffs**: Modify only the lines that need to change. Never reprint an entire file for a localized tweak.
2. **Context Isolation**: Workers receive only their designated chunk and the exact files needed—never the whole repository.
3. **Taste Before Code**: Establish typography, color palettes, spacing, and interaction principles before authoring any UI markup.
4. **Senior Review Loops**: Automated 5-point audits (correctness, security, readability, errors, tests) iterate up to 3 times until production-ready.
5. **Teach While Building**: Every completed milestone records a brief educational note (concept, analogy, hands-on challenge) in `LEARNING.md`.

---

## Universal Workflow

All agent actions flow deterministically through [`AGENTS.md`](AGENTS.md):

```text
[ User Prompt ]
       │
       ▼
1. prompt-optimizer ──> Rewrites request into clear spec, assumptions & non-goals
       │
       ▼
2. planner          ──> Decomposes spec into atomic chunks in TASKS.md
       │
       ▼
3. design-taste     ──> (UI only) Generates DESIGN.md tokens & visual concept
       │
       ▼
4. orchestrator     ──> Dispatches chunks to roles (max 5 parallel, or sequential)
       │
       ▼
5. diff-guard       ──> Enforces surgical, zero-slop edits on every file change
       │
       ▼
6. reviewer         ──> Senior engineer 5-point audit loop (max 3 cycles)
       │
       ▼
7. teach-mode       ──> Appends concise lesson note to LEARNING.md (<120 words)
```

---

## Skills Catalog

Each skill in `skills/` is a modular, self-contained markdown specification with YAML frontmatter, strictly free of emojis. Length is fine. Structure for skimming, split large topics into files that load on demand, and keep AGENTS.md short because it is always loaded:

- [`skills/prompt-optimizer/SKILL.md`](skills/prompt-optimizer/SKILL.md): Compresses requests into specs, clarifies assumptions, and caps blocking questions to 3.
- [`skills/planner/SKILL.md`](skills/planner/SKILL.md): Breaks requirements into atomic chunks and maintains `TASKS.md`.
- [`skills/design-taste/SKILL.md`](skills/design-taste/SKILL.md): Enforces palette, typography, spacing, motion, and optional 3D/canvas directions before coding.
- [`skills/orchestrator/SKILL.md`](skills/orchestrator/SKILL.md): Dispatches chunks across roles, enforces minimal context boundaries, and serializes shared files.
- [`skills/diff-guard/SKILL.md`](skills/diff-guard/SKILL.md): Guards diff sizes, blocks unsolicited refactors, and ensures surgical code updates.
- [`skills/reviewer/SKILL.md`](skills/reviewer/SKILL.md): Audits correctness, security, tests, readability, and error handling in a 3-loop feedback cycle.
- [`skills/teach-mode/SKILL.md`](skills/teach-mode/SKILL.md): Generates educational walkthroughs with real-world analogies and mini-challenges.

---

## Role Specialization

Specialist definitions in `roles/` enforce strict boundaries so agents never step on each other:

- [`roles/frontend.md`](roles/frontend.md): UI components, responsive layouts, accessibility, and design token integration.
- [`roles/backend.md`](roles/backend.md): Domain business logic, state machines, algorithms, and compute services.
- [`roles/database.md`](roles/database.md): Schema migrations, indexes, integrity constraints, and query optimization.
- [`roles/api.md`](roles/api.md): Route controllers, validation schemas, response serialization, and auth guards.
- [`roles/flex.md`](roles/flex.md): Tooling, build pipelines, CI configurations, and integration tests.

---

## Installation by Tool

Follow the step-by-step setup adapter for your AI tool:

| Tool | Adapter Guide | Supported Concurrency |
|---|---|---|
| **Claude** | [`adapters/claude.md`](adapters/claude.md) | Sequential fallback |
| **OpenAI Codex** | [`adapters/codex.md`](adapters/codex.md) | Sequential fallback |
| **Google Antigravity** | [`adapters/antigravity.md`](adapters/antigravity.md) | Native parallel subagents (up to 5 workers) |
| **Cursor** | [`adapters/cursor.md`](adapters/cursor.md) | Composer / sequential fallback |

### Quick Start (Any Project)

Clone or copy the files into your project:

```bash
git clone https://github.com/VinayKhandia/no-slop.git
cp -r no-slop/skills ./skills
cp -r no-slop/roles ./roles
cp no-slop/AGENTS.md ./AGENTS.md
```

Then prompt your agent:
> *"Follow the no-slop protocol defined in AGENTS.md to implement [your feature]."*

---

## Worked Example

Inspect the complete worked example in [`examples/`](examples/):
- [`examples/TASKS.md`](examples/TASKS.md): Live task tracking board showing role assignments and statuses.
- [`examples/DESIGN.md`](examples/DESIGN.md): Systems-engineer portfolio aesthetic with custom palette and orthographic wireframe concept.
- [`examples/LEARNING.md`](examples/LEARNING.md): Real-world lesson notes with analogies and challenges for each task chunk.

---

## Contributing

We welcome community contributions! Please review [`CONTRIBUTING.md`](CONTRIBUTING.md) for frontmatter schema, token efficiency, and authoring guidelines.

## License

This project is open-source under the [MIT License](LICENSE). Copyright (c) 2026 Vinay Khandia.
