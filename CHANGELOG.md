# Changelog

All notable changes to the AI Dev Exoskeleton are recorded here.
Versioning is informal (this is a methodology, not a package): the version marks a
coherent snapshot you can copy into a repo and expect the docs to match.

## [0.1.0] — 2026-07-30 — first public release

Initial public version, distilled from ~200–300 hours across 78 personal
agentic-engineering sessions and refined through workshops at two companies.

- **Agents** (universal roles): planner, implementer, reviewer, explorer, debugger.
- **Commands**: build-context, start-debug, review-walkthrough, adversarial-review.
- **Guides**: PLAYBOOK (the Laws), workflows (feature, debug, refactor, onboarding),
  pre/post-session checklists, field-notes.
- **Project knowledge** lives in `docs/context/`; the exoskeleton itself stays universal.
- Harness adapters: canonical `AGENTS.md` with `CLAUDE.md` / `GEMINI.md` pointers.

### Upgrading a copied exoskeleton
This system is copied into each repo, so copies drift from the source. To upgrade a
project, replace its `.ai-dev-exoskeleton/` folder with the new version and re-check the
repo's `AGENTS.md` pointer. Your `docs/context/` (project knowledge) is untouched.
