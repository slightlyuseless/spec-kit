# AGENTS.md

> This repository follows the [agents.md](https://agents.md/) convention. Treat this file as the authoritative onboarding and operating manual for any AI assistant executing work inside Spec Kit.

## Scope & Source of Truth

- **Audience:** Codex running inside VS Code, plus maintainers preparing the Codex distribution of Spec Kit.
- **Coverage:** The entire repository. A matching consumer-facing copy is generated at `.codex/AGENTS.md`; keep both synchronized.
- **Workflow anchor:** Always start in this file. All other docs (`README.md`, `docs/*.md`, prompts) elaborate on the guidance captured here.

## Quickstart (Codex in VS Code)

1. **Bootstrap the workspace** – Run `specify init <project-name>` (or `specify init --here`) from the VS Code terminal.
2. **Load the Codex entry point** – Open `.codex/AGENTS.md` inside the Codex extension to ingest these instructions.
3. **Run the slash-command workflow** in order:
   1. `/speckit.constitution`
   2. `/speckit.specify`
   3. `/speckit.plan`
   4. `/speckit.tasks`
   5. `/speckit.implement`
   6. Optional helpers: `/speckit.clarify`, `/speckit.checklist`, `/speckit.analyze`
4. **Iterate through prompts, not manual edits** – Regenerate specs, plans, and tasks via their commands to keep artifacts consistent.

## Collaboration Principles

- Specs are the contract. Update specifications before revising plans or tasks.
- Implementation decisions belong in `/specs/<feature>/plan.md` and `/specs/<feature>/tasks.md` so Codex always sees current context.
- Use helper commands (clarify/checklist/analyze) whenever ambiguity or coverage gaps arise.
- Preserve generated history; avoid deleting prior spec/plan/task revisions unless part of a documented workflow.

## Command & Prompt Maintenance

- Authoritative prompt sources live in `templates/commands/` and `templates/codex/AGENTS.md`.
- Regenerate `.codex/commands/*.md` and `.codex/AGENTS.md` through the release tooling; do not hand-edit generated artifacts in downstream projects.
- Update root documentation (`README.md`, `docs/installation.md`, `docs/local-development.md`) whenever the workflow or command list changes.

## Repository Guardrails

- Any change to `src/specify_cli/__init__.py` **must** include a matching version bump in `pyproject.toml` plus a `CHANGELOG.md` entry.
- Run `uv build` (optional) after substantial CLI or prompt changes to confirm packaging still succeeds.
- Keep Codex-specific instructions accurate before publishing releases or templates.

## Packaging Notes (Codex Distribution)

Release bundles produced by `.github/workflows/scripts/create-release-packages.sh` must retain this structure:

```
.codex/
  AGENTS.md         # Copied from templates/codex/AGENTS.md
  commands/         # Populated from templates/commands/*.md
.specify/
  memory/
  scripts/
  templates/
```

Adjust the script if you rename directories or add new assets so the Codex archive remains coherent.

## Historical Agent Archive

The project previously supported additional assistants. Use this reference if you need to restore them in a fork.

| Agent | Directory | Format | Interface | Notes |
|-------|-----------|--------|-----------|-------|
| **Codex (current)** | `.codex/commands/` + `.codex/AGENTS.md` | Markdown | VS Code Extension | Primary, maintained distribution |
| Claude Code | `.claude/commands/` | Markdown | `claude` CLI | Legacy Anthropic workflow |
| Gemini CLI | `.gemini/commands/` | TOML | `gemini` CLI | Legacy Google workflow |
| GitHub Copilot | `.github/prompts/` | Markdown | VS Code Extension | Deprecated prompts |
| Cursor | `.cursor/commands/` | Markdown | `cursor-agent` CLI | Deprecated CLI |
| Qwen Code | `.qwen/commands/` | TOML | `qwen` CLI | Deprecated CLI |
| opencode | `.opencode/command/` | Markdown | `opencode` CLI | Deprecated CLI |
| Windsurf | `.windsurf/workflows/` | Markdown | Windsurf IDE | Deprecated IDE workflows |
| Kilo Code | `.kilocode/rules/` | Markdown | Kilo Code IDE | Deprecated IDE workflows |
| Auggie CLI | `.augment/rules/` | Markdown | `auggie` CLI | Deprecated CLI |
| Roo Code | `.roo/rules/` | Markdown | Roo IDE | Deprecated IDE workflows |
| CodeBuddy CLI | `.codebuddy/commands/` | Markdown | `codebuddy` CLI | Deprecated CLI |
| Amazon Q Developer CLI | `.amazonq/prompts/` | Markdown | `q` CLI | Deprecated CLI |
| Amp | `.agents/commands/` | Markdown | `amp` CLI | Deprecated CLI |

## Re-enabling Additional Agents

1. Update `AGENT_CONFIG` in `src/specify_cli/__init__.py` with the new assistant metadata.
2. Refresh CLI help text and documentation (`README.md`, `docs/installation.md`, etc.).
3. Add or modify prompt templates under `templates/commands/` and extend the release script to package the new assets.
4. Increment the package version in `pyproject.toml` and append a `CHANGELOG.md` entry documenting the change.

Maintain this file as the canonical reference before shipping updates to end users or templates.
