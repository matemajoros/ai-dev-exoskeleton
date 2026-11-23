# Review: feature-flag red phase in heavy rigor

> Independence caveat: no subagent tool was available, so the same model that implemented
> this change reviewed it, in a separate step. This is NOT an independent review.

### Acceptance
- Flag protocol in `heavy-mode.md` (off-red, on-green, removed-green, never ships) — met — `.ai-dev-exoskeleton/references/heavy-mode.md` `### Feature-flag red phase`.
- Skipped for refactoring/config/docs/no-behaviour; reason in report when no flag fits — met — same section, first paragraph.
- Reviewer records both runs under `### Evidence`; missing/empty/unrelated proof is WARNING — met — `## Reviewer`, flag bullet.
- Agent files, light path, rule 2 unchanged — met — `git diff main --stat` lists no `agents/`, README or guides file.
- VERSION and CHANGELOG say 0.4.0 — met — see Evidence.

### CRITICAL
- none

### WARNING
- none

### NOTE
- `heavy-mode.md` Reviewer bullet: "a flag left in the code -> CRITICAL" is not in CONTEXT.md, which only names the WARNING for missing proof. It is an addition by the implementer; the owner may soften it to WARNING.
- The flag section sits under `## Implementer` as an `###` heading, so it is read only under heavy, as required.
- README/PLAYBOOK checked: PLAYBOOK says heavy "adds ... the gates in heavy-mode.md", still true; the README file count (23 of 30) is unaffected because no file was added. No edit needed.

### Missing Tests
- Not applicable: plain-text repo, no test command. The protocol itself was not exercised on a real task.

### Evidence
```
$ git diff main --name-only
.ai-dev-exoskeleton/VERSION
.ai-dev-exoskeleton/references/heavy-mode.md
CHANGELOG.md
$ cat .ai-dev-exoskeleton/VERSION   -> 0.4.0
$ rg -n "^## \[" CHANGELOG.md       -> 15:## [0.4.0] — 2026-11-23 ...
$ git diff main --stat: 3 files changed, 38 insertions(+), 1 deletion(-)
```
No red/flag run applies: no behaviour code changed.

### Risk
low — text-only change to one heavy-only reference file; light path untouched. Same-model review lowers confidence in wording clarity.

### Summary
Safe to merge after the owner decides on the CRITICAL-for-leftover-flag addition.
