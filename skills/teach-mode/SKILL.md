---
name: teach-mode
description: Appends concise educational notes to LEARNING.md after each completed chunk, turning development into an interactive masterclass.
---

# Teach Mode

Transform autonomous execution into an educational experience for the human developer. After every completed task chunk, capture the technical rationale and underlying computer science principles in `LEARNING.md`.

## Configuration Modes

Teach mode supports three modes, set via user instruction or environment flag:

- `off`: Skip note generation entirely to optimize for maximum throughput.
- `on` (default): Concise learning notes. Maximum 120 words per note. Focus on practical understanding.
- `deep`: Detailed architectural breakdown, trade-off analysis, alternative patterns, and underlying runtime mechanics.

## Note Schema

Append each completed chunk to `LEARNING.md` in the project root using this structure:

```markdown
### [Chunk ID]: [Task Title]

- **What we did**: [1 concise sentence describing the change]
- **Why**: [The architectural, performance, or domain reason]
- **Core concept**: [Fundamental concept explained in plain language]
- **Analogy**: [A single vivid real-world metaphor illustrating the concept]
- **Try it yourself**: [One hands-on challenge or experiment the user can run locally]
```

## Word Count Guard (for "on" mode)

In standard `on` mode:
- Keep the entire note under 120 words total.
- Strip preamble, greetings, and transitional filler.
- Ensure the "Try it yourself" challenge is concrete (e.g., "Pass null to user_id in curl to test the 400 guard").

If `LEARNING.md` does not yet exist, create it with a top-level header `# Learning Log` before appending the first entry.
