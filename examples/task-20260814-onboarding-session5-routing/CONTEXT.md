# Onboarding Session 5 — Workflow Routing — Context

## Jira / Ticket
—

## Business Requirements
- Session 5 of onboarding ("First Real Task as Validation") currently hands the reader a
  fixed `MODE:`/`SCOPE:`/`CONTEXT:`/`DONE WHEN:` prompt block instead of pointing them at
  the feature, debug, and refactor workflow guides that already exist for exactly this kind
  of work.
- The first real task after onboarding should exercise the actual workflow the reader will
  keep using afterward, not a one-off prompt template that gets thrown away.
- Keep the first task small — this session validates the context just built; it is not the
  start of the roadmap.

## UX / Design Decisions
- Replace the fixed prompt with a routing table: work type → workflow name → path. The
  reader picks a row instead of filling in a template from scratch.
- Add one guardrail sentence directly under the table: keep the first one small (one
  feature phase, one bug, one contained refactor).
- Add a fallback for work that fits none of the three rows, pointing at the pre-session
  checklist's copy-paste openers rather than leaving the reader stuck.

## Technical Decisions
- Table rows point only at files that already exist:
  `.ai-dev-exoskeleton/guides/workflows/feature.md`, `debug.md`, `refactor.md`. No new
  workflow doc is created.
- The fallback points at `.ai-dev-exoskeleton/guides/checklists/pre-session.md`.
- The post-session review block immediately below Session 5 (the four bullets on whether
  AGENTS.md and docs/context/ gave the agent enough) is left as-is — same questions, same
  file reference.

## Open Questions That Were Resolved
- Q: Should the fallback exist, or are the three rows exhaustive? → A: Keep a fallback —
  not every first task is cleanly a feature, a bug, or a refactor, and the pre-session
  checklist already carries copy-paste openers for that case.
- Q: Does routing replace the workflow docs themselves? → A: No. `feature.md`, `debug.md`,
  and `refactor.md` are unchanged; only the pointer to them changes.

## Exclusions
- Sessions 1–4 of onboarding — untouched.
- The workflow docs themselves (`feature.md`, `debug.md`, `refactor.md`) and the
  pre-session checklist — untouched, only referenced by path.
- The post-session review block, the Checklist Summary, and the Time Estimate table later
  in the same file — untouched.

## Rigor
light — one guide file, one section, no reviewer would be asked
