# Feature-flag red phase in heavy rigor

## Goal
Add the feature-flag red phase to the heavy-rigor implementer and reviewer sections, and release it as 0.4.0.

## Current State
`references/heavy-mode.md` has Planner, Implementer, Hardening pass and Reviewer sections; none mentions a flag. Version is 0.3.0.

## Target State
Under heavy, a behaviour-changing task follows the flag protocol (flag off -> red, flag on -> green, flag removed -> green) or the report says why not. The reviewer checks both runs and warns when the proof is missing. `VERSION` is 0.4.0 with a matching changelog entry.

## Phases

### Phase 1: Flag protocol, version, changelog
**Scope:** `.ai-dev-exoskeleton/references/heavy-mode.md`, `.ai-dev-exoskeleton/VERSION`, `CHANGELOG.md`
**Changes:**
- [ ] heavy-mode.md `## Implementer`: add the flag protocol (when it applies, six steps, flag never ships, report lines, why it complements rule 2)
- [ ] heavy-mode.md `## Reviewer`: check flag-off red and flag-on green runs, record under `### Evidence`, WARNING when missing, empty or unrelated
- [ ] VERSION: 0.4.0
- [ ] CHANGELOG.md: `[0.4.0]` entry in the 0.3.0 format
- [ ] README/PLAYBOOK: change only a statement that became untrue (checked: none found; PLAYBOOK only says heavy "adds the gates in heavy-mode.md", still true)
**Verify:** re-read changed files; `rg -n -i "flag|red phase"` for consistent wording; VERSION equals the CHANGELOG heading; `git diff --name-only main` lists only allowed files.
**Rollback:** `git revert` the commit, or drop the branch.
**Depends on:** —

## Acceptance
- [ ] WHEN an implementer on a heavy, behaviour-changing task reads `heavy-mode.md` -> THEN it finds the flag protocol with the off-red, on-green, removed-green sequence and the "flag never ships" rule.
- [ ] WHEN the task is refactoring, configuration, documentation, or has no behaviour change, or no flag fits -> THEN the text says to skip it and state why in the report.
- [ ] WHEN a reviewer on a heavy task finds no, empty or unrelated red/green proof for a behaviour change -> THEN the text says WARNING; the runs go under `### Evidence`.
- [ ] WHEN `agents/*.md` and the light path are read -> THEN they are unchanged, and rule 2 still stands.
- [ ] WHEN `VERSION` and `CHANGELOG.md` are read -> THEN both say 0.4.0.

## Risks
- Wording clashes with rule 2 or "vertical slices": state that the protocol is an extra proof, not a replacement, and still one test at a time.
- A flag that leaks into the diff: the final step removes it and the reviewer checks for leftovers.

## Open Questions
- None.
