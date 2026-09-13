# AGENTS.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## `/docs` Organization

- Use `docs/PLAN.md` as the primary SDD + TDD planning template (English); never overwrite it with a concrete plan. `docs/PLAN-es.md` is an optional Spanish-language alternative, kept for users who prefer it — use it only when explicitly requested, and don't treat it as requiring sync with `PLAN.md`.
- When creating a plan, generate a sibling file `docs/PLAN-<topic>.md` with a descriptive kebab-case slug, based on the English template by default (or the Spanish one only if explicitly requested). If one already exists for the same goal, update it instead of duplicating it.
- Keep only the template and active `PLAN-*.md` plans in the root of `docs/`; once a plan is completed, move it to its corresponding topic subfolder.
- Define the story, assumptions, requirements, and acceptance criteria first (SDD); derive the tests from them and execute each slice with RED → GREEN → REFACTOR (TDD).
- Before adding or moving documentation, read its content and place it in the appropriate topic subfolder.
- Don't leave other files loose in the root of `docs/`; create a topic subfolder whenever no suitable category exists.
