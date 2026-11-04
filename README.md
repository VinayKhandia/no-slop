# no-slop

A markdown-only plugin that makes AI coding agents work like a studio with a client: they plan first, pause at gates to ask for your taste decisions, use your real assets, keep diffs small, and check their own work visually before saying "done".

MIT licensed. No runtime, no dependencies. Everything is Markdown the agent reads.

## Status

- Tested on: Antigravity.
- Manifests included, not yet tested: Claude Code and Codex.
- Output quality depends heavily on the model you run it with. Weaker models skip steps or build shallow results. This is a work in progress, not a guarantee.

## What it does

- **Gated workflow for new sites and apps.** The agent stops at each gate (intake, direction, type and color, motion and story, hero, sections, final) and asks you. It does not build before Gate 0 is approved. Say the word "autopilot" to skip the pauses.
- **Prompt optimizer.** Turns a rough request into a structured BRIEF.md before any work starts.
- **Client collaboration.** Reference boards by slot (components, cursors, text animation, backgrounds and 3D environments, scroll and transitions), palette options that are not just the literal reading of a name, previews you can open locally, and a DECISIONS.md that records every choice.
- **Design and motion libraries.** Eleven style recipes, a cursor library, a motion kit (text, card, button, environment, transitions), a fluid-scroll pattern, and 3D environment patterns including a helix room.
- **Visual QA.** Screenshots, frame-time checks and a review pass before the agent reports done.
- **Minimal edits.** A diff guard keeps changes small for small requests. Quick fixes do not trigger the gates.
- **Teach mode.** Optional explanations while it builds.

## Skills

asset-intake, client-collab, design-taste, diff-guard, motion-craft, no-slop-start, orchestrator, planner, prompt-optimizer, reference-teardown, reviewer, scene-3d, storyboard, teach-mode, visual-qa.

Skills load on demand, so unused ones cost almost no context.

## Install

### Antigravity (tested)

```
git clone https://github.com/VinayKhandia/no-slop.git
mkdir -p ~/.gemini/config/plugins
rsync -a --exclude .git no-slop/ ~/.gemini/config/plugins/no-slop/
```

Restart the agent panel, then check that no-slop skills appear in Customizations.

### Claude Code (untested)

```
/plugin marketplace add VinayKhandia/no-slop
/plugin install no-slop
```

The manifests follow the Claude Code plugin layout, but I have not run them yet. The always-on rules in `rules/AGENTS.md` are not known to load in Claude Code, so the `no-slop-start` skill triggers the gates instead.

### Codex (untested)

Manifests are in .codex-plugin/ and .agents/plugins/. The exact marketplace command may differ by version, so check `codex plugin --help`.

### Other tools

The skills are plain Markdown in the open SKILL.md format. Tools that read `SKILL.md` folders (such as Qwen Code, Kimi Code and Grok Build, per their docs) can use them by copying `skills/` into their skills directory (for example `.agents/skills/`). Not tested here.

## How to prompt

Be specific about the product, audience and feel. For example:

```
Build an immersive 3D landing page for my perfume brand Noir.
Photos are in assets/. Collab mode.
```

The agent will ask questions and show previews. Answer them, point at references you like, and say what you would change.

For a small edit, just ask:

```
Change the main button color to red.
```

## Repo layout

- `AGENTS.md`: source rules (copied to `rules/AGENTS.md` by `scripts/sync-rules.sh`)
- `skills/`: the skills above
- `roles/`: role notes for frontend, backend, database, API and flex work
- `plugin.json`, `assets/`: Antigravity and Codex-style manifest
- `.claude-plugin/`: Claude Code manifests

## Known limitations

- Sub-agent or parallel work depends on whether your tool actually dispatches agents. The roles are guidance, not a guarantee of parallelism.
- Backend, database, API and integration skills are still thin.
- Realistic product 3D needs real assets (photos, turntable frames or a .glb). Without them the agent uses placeholders and labels them.
- The gate workflow costs more tokens than a plain prompt. It trades tokens for fewer redo rounds. A lighter mode is planned.
- No benchmark yet comparing results with and without the plugin.

## Contributing

See CONTRIBUTING.md. Edit `AGENTS.md`, not `rules/AGENTS.md`, then run `scripts/sync-rules.sh`.

## License

MIT, Copyright (c) 2026 Vinay Khandia.
