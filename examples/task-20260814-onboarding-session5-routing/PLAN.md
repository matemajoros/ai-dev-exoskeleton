# Onboarding Session 5 — Workflow Routing

## Goal
Replace Session 5's hardcoded `MODE:`/`SCOPE:`/`CONTEXT:`/`DONE WHEN:` prompt with a table
that routes the reader to the feature, debug, or refactor workflow, plus a fallback for
work that fits none of the three.

## Current State
`.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md`, Session 5 ("First Real
Task as Validation"), hands the reader one fixed prompt block:

```
MODE: debug (or implement)
SCOPE: [small, well-defined area]
CONTEXT: First task on this project — validating my agentic engineering setup.
DONE WHEN: Task completed, tests pass, and the setup felt effective.
```

It never points at `.ai-dev-exoskeleton/guides/workflows/feature.md`, `debug.md`, or
`refactor.md` — the workflows the reader is meant to use for real work from this point
forward.

## Target State
The same section opens with a three-row table (work type → workflow → path), one sentence
telling the reader to keep the first task small, and a fallback to
`pre-session.md`'s copy-paste openers for anything none of the three rows cover. The
post-session review bullets directly below are unchanged.

## Phases

### Phase 1: Rewrite Session 5
**Scope:** `.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md` (Session 5
section only)
**Changes:**
- [ ] Remove the hardcoded `MODE:`/`SCOPE:`/`CONTEXT:`/`DONE WHEN:` block
- [ ] Add the routing table: feature/change → `feature.md`, bug/error → `debug.md`,
      move/rename/restructure → `refactor.md`
- [ ] Add the "keep the first one small" guardrail sentence
- [ ] Add the fallback sentence to `pre-session.md` for work that fits none of the three
      rows
- [ ] Leave the post-session review bullets directly below untouched

**Verify:** No test command applies — this is a markdown-only change to a guide. Verify is
a human read-through of Session 5 top to bottom, plus:
`fd . .ai-dev-exoskeleton/guides/workflows` lists `feature.md`, `debug.md`, `refactor.md`
— the three paths the table names — and
`fd . .ai-dev-exoskeleton/guides/checklists` lists `pre-session.md` — the fallback path.
**Rollback:** `git restore .ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md`
**Depends on:** —

## Acceptance
- [ ] WHEN a reader reaches Session 5 of the onboarding guide → THEN they see a table
      naming a workflow and a path for feature work, bug/error work, and restructuring
      work, not a fixed prompt block
- [ ] WHEN a reader's first task fits none of the three rows → THEN the guide tells them
      where to fall back (the pre-session checklist) instead of leaving them stuck
- [ ] WHEN a reader follows any of the three paths in the table → THEN the file it names
      exists at that path

## Risks
- **Table drifts from the workflow docs it names.** If `feature.md`, `debug.md`, or
  `refactor.md` is ever renamed or removed, the table silently points nowhere. Nothing in
  this change enforces that the two stay in sync — it relies on whoever edits a workflow
  doc later to notice.

## Open Questions
- —
