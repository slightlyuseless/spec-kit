# Spec Kit × Codex Workspace Guide

> This workspace ships with the [agents.md](https://agents.md/) contract. Read and follow every section before executing commands.

## Scope

- Applies to all work performed with Codex inside this repository.
- Mirrors the root `AGENTS.md`; refer there for maintainer-specific responsibilities.

## Quickstart

1. **Provision the workspace** – Run `specify init <project-name>` (or `specify init --here`) from the VS Code terminal.
2. **Load this file in Codex** – Use the Codex sidebar to open `.codex/AGENTS.md` so the agent ingests the canonical instructions.
3. **Execute the slash-command workflow** in this order:
   1. `/speckit.constitution`
   2. `/speckit.specify`
   3. `/speckit.plan`
   4. `/speckit.tasks`
   5. `/speckit.implement`
   6. Optional helpers: `/speckit.clarify`, `/speckit.checklist`, `/speckit.analyze`

## Working Agreement

- Specifications are authoritative; update them before modifying plans or tasks.
- Keep implementation rationale within `/specs/<feature>/plan.md` and `/specs/<feature>/tasks.md`.
- Regenerate artifacts via their commands—do not hand-edit generated specs, plans, or tasks.
- Use helper commands whenever requirements are ambiguous or coverage feels incomplete.

## Maintainer Touchpoints

- Prompt sources live in `templates/commands/` (slash commands) and this template.
- Changes to CLI behavior (`src/specify_cli/__init__.py`) require a version bump and changelog entry.
- Run `uv build` (optional) after substantial changes to validate packaging.

## Reference Material

- `README.md` – End-to-end overview of the Codex distribution.
- `docs/installation.md` – Environment setup guidance.
- `docs/local-development.md` – Tips for contributing to Spec Kit locally.
