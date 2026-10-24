---
name: diff-guard
description: Enforces minimal, surgical file edits and eliminates slop, unwarranted refactors, and context-wasting rewrites.
---

# Diff Guard

Protect the repository from code bloat, unsolicited refactoring, and excessive diff churn. Diff Guard must be respected on every single code modification.

## Invariant Rules

1. **Surgical Edits Only**:
   - Change strictly the lines directly related to the active task chunk.
   - Use targeted edit tools (e.g., replacement blocks, line-based sed/edits, or AST modifiers).
   - Never print or rewrite an entire 300-line file to adjust a 4-line function.
2. **Zero Slop**:
   - Do NOT add decorative or obvious comments (e.g., `// Constructor`, `// Returns the id`).
   - Do NOT insert unrequested helper functions, hypothetical abstractions, or premature utility layers.
   - Do NOT update adjacent code formatting, variable renames, or style preferences outside the task scope.
   - Do NOT add unsolicited dependencies or packages unless explicitly specified in `TASKS.md`.
3. **Preserve Existing Structure**:
   - Keep existing variable naming conventions, export patterns, and indentation intact.
   - Preserve existing comments, licenses, and docstrings untouched.

## Pre-Completion Verification Check

Before signaling that an edit or chunk is ready for review:

1. **Inspect Git Diff**:
   - Review `git diff --stat` and the exact line diffs.
2. **Diff Size vs. Task Size Evaluation**:
   - Compare the diff footprint against the single task objective in `TASKS.md`.
   - If a 10-line logic fix resulted in a 150-line diff, identify what was rewritten unnecessarily.
3. **Surgical Reversion**:
   - Immediately revert any changes that do not directly contribute to fulfilling the task chunk.
   - Strip out extraneous files, debug logging statements, or test scaffolding created solely for ad-hoc manual verification.
