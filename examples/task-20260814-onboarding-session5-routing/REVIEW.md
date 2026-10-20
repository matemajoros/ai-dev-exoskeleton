## Review: Onboarding Session 5 — workflow routing table

### Acceptance
- A reader reaching Session 5 sees a table naming a workflow and a path for feature,
  bug/error and restructuring work, not a fixed prompt block — met — the three-row table
  sits at `.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md:392-396`, and
  Session 5 holds no fenced block
- A first task that fits none of the rows has somewhere to fall back — met — the fallback
  sentence names the pre-session checklist by path
  (`.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md:401-403`)
- Every path in the table names a file that exists — met — `fd` lists `feature.md`,
  `debug.md` and `refactor.md` at the paths the rows give, and `pre-session.md` at the
  fallback's path (Evidence)

### CRITICAL
—

### WARNING
—

### NOTE
- [`.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md:401-403`] The fallback
  sentence says the pre-session checklist "holds copy-paste session openers for plan,
  implement, and debug" — three of the four. `pre-session.md:74` also has a
  `### Feature Session (start here)` template, which this sentence doesn't mention. Harmless
  today, since a feature-shaped task is already routed by row 1 of the new table to the
  fuller `feature.md` workflow — but the checklist's own template is labelled "start here"
  for the same case, so the two entry points now overlap and the fallback text is not quite
  describing what pre-session.md actually contains.

### Missing Tests
- None — this is a markdown-only guide change with no test suite to extend. The check is
  the human read-through and the path listings `PLAN.md`'s Verify already specifies.

### Evidence
```
$ fd . .ai-dev-exoskeleton/guides/workflows
.ai-dev-exoskeleton/guides/workflows/debug.md
.ai-dev-exoskeleton/guides/workflows/feature.md
.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md
.ai-dev-exoskeleton/guides/workflows/refactor.md

$ fd . .ai-dev-exoskeleton/guides/checklists
.ai-dev-exoskeleton/guides/checklists/post-session.md
.ai-dev-exoskeleton/guides/checklists/pre-session.md
```

### Risk
low — one section of one guide, markdown only; every path it names exists (Evidence) and
nothing outside Session 5 changed

### Summary
Safe to merge. The three table rows all resolve to files that exist
(`.ai-dev-exoskeleton/guides/workflows/feature.md`, `debug.md`, `refactor.md`), the
fallback path (`pre-session.md`) exists, and the post-session review block below is
untouched as intended. One NOTE on a wording nit in the fallback description; nothing
blocks acceptance.
