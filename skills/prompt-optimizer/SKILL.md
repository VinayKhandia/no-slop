---
name: prompt-optimizer
description: Transforms vague or verbose user requests into concise, unambiguous technical specifications with explicit assumptions.
---

# Prompt Optimizer

Before running any planners, orchestrators, or code edits, transform the raw request into an unambiguous technical target.

## Objectives

1. Eliminate ambiguity and reduce fluff to minimize downstream token costs.
2. Establish explicit assumptions so execution can proceed without stalling.
3. Ask clarifying questions only when missing information represents an absolute blocker.

## Procedure

1. **Ingest Request**: Read the user's prompt and extract primary functional requirements, constraints, and non-goals.
2. **Compress and Formalize**:
   - Rewrite the prompt into a technical spec of 5-15 lines.
   - List key assumptions (e.g., chosen frameworks, storage format, browser/runtime targets).
   - Define concrete boundaries of what will NOT be built in this iteration.
3. **Question Gate**:
   - If critical information is missing and cannot be reasonably assumed, ask at most 3 clarifying questions.
   - If sensible default conventions exist (e.g., SQLite for local DB, standard REST conventions, standard CSS variables), adopt the default, declare it under assumptions, and proceed immediately. Do not block on non-critical preferences.

## Specification Output Format

Present the optimized spec to the workflow using this format:

```markdown
### Target Specification
- Goal: [1-2 sentences]
- Scope: [Core deliverables]
- Non-Goals: [Explicit exclusions]

### Assumptions
- [Assumption 1]
- [Assumption 2]
```

Once the spec is confirmed or assumed, transfer execution directly to the planner skill.
