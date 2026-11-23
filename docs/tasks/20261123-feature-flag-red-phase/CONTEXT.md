# Feature-flag red phase in heavy rigor — Context

## Jira / Ticket
—

## Business Requirements
- Add the cc-sdd style **feature-flag red phase** to the Exoskeleton as an extra, mechanical proof that a test checks the new behaviour: the implementer adds a flag (default off), writes the tests, runs them with the flag off and sees them FAIL, switches the flag on, writes the implementation, sees them PASS, then removes the flag and sees them still PASS.
- It applies under **heavy rigor** only. Under heavy it is **required for behaviour-changing tasks** when a flag can be introduced in a sensible way in the project; otherwise the implementer states in the report why it was not used. It is skipped for refactoring, configuration, documentation, and any task with no behaviour change.
- The flag is temporary: it is removed before the phase ends. It never ships.
- The implementer's report gets the flag-off red run and the flag-on green run (test command and output) next to the existing red-run line; the reviewer checks them and records them under `### Evidence`. A missing, empty or unrelated red/green proof on a behaviour-changing task under heavy is a **WARNING**.

## UX / Design Decisions
- Keep the method small: no new agent file, no new command, no new top-level guide.
- Wording stays in the Exoskeleton's own style: short, imperative, rule plus one-line reason.

## Technical Decisions
- Edit only `.ai-dev-exoskeleton/references/heavy-mode.md`: the `## Implementer` section (the flag protocol) and the `## Reviewer` section (the evidence check and the WARNING). Heavy-only content belongs there, because that file is read only when `CONTEXT.md` has `## Rigor: heavy`.
- Do not change `agents/implementer.md` rule 2 ("No behaviour ships without a test you have seen fail on it"). The flag protocol is a stronger, optional-by-rigor way to meet it, not a replacement. Do not make TDD or "tests first" mandatory.
- Raise `.ai-dev-exoskeleton/VERSION` from `0.3.0` to `0.4.0` and add a `0.4.0` entry to `CHANGELOG.md` (same format as the `0.3.0` entry; informal versioning).
- Check the README and PLAYBOOK for statements the change makes untrue (for example the heavy-mode description or file counts) and fix only those.
- Git: work only in this worktree on `improvement/feature-flag-red-phase` (based on `main`). Do not touch `main` or the `v0.3.0` tag: the dissertation experiment uses the frozen `0.3.0` (commit 77d90b4). Push is not available from this session; commit locally and export a patch.

## Open Questions That Were Resolved
- Q: Is a new walkthrough document needed? → A: No. The earlier "walkthrough" was a misunderstanding of "git worktree".
- Q: Mandatory or optional under heavy? → A: Mandatory for behaviour-changing tasks when a flag fits the project; otherwise justify in the report. Reviewer: WARNING if the proof is missing.
- Q: Bump the version and write a changelog? → A: Yes, on this branch (0.4.0).

## Exclusions
- No change to the light rigor path.
- No change to the three agent files (`planner`, `implementer`, `reviewer`) or to rule 2.
- No new files in `.ai-dev-exoskeleton/`.
- No change to `main`, `v0.3.0`, or anything outside this worktree. No merge, no push.

## Rigor
light — a small, text-only change to one reference file plus version bump and changelog; no other human review requested.
