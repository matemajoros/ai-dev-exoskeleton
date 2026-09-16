## Review: Onboarding Session 5 — workflow routing table

### CRITICAL
—

### WARNING
—

### NOTE
- [`.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md:263-265`] The fallback
  sentence says the pre-session checklist "holds copy-paste session openers for plan,
  implement, and debug" — three of the four. `pre-session.md:78` also has a
  `### Feature Session (start here)` template, which this sentence doesn't mention. Harmless
  today, since a feature-shaped task is already routed by row 1 of the new table to the
  fuller `feature.md` workflow — but the checklist's own template is labelled "start here"
  for the same case, so the two entry points now overlap and the fallback text is not quite
  describing what pre-session.md actually contains.

### Missing Tests
- None — this is a markdown-only guide change with no test suite to extend. The check is
  the human read-through and the path greps `PLAN.md`'s Verify already specifies.

### Summary
Safe to merge. The three table rows all resolve to files that exist
(`.ai-dev-exoskeleton/guides/workflows/feature.md`, `debug.md`, `refactor.md`), the
fallback path (`pre-session.md`) exists, and the post-session review block below is
untouched as intended. One NOTE on a wording nit in the fallback description; nothing
blocks acceptance.
