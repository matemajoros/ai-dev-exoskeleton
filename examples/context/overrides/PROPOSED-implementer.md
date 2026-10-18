# PROPOSED override: implementer.md

> Inert. Agents read `docs/context/overrides/implementer.md`, never a `PROPOSED-` file;
> activating this one is a rename, and the rename is a human's call
> (.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md:302-304).

## Rule overridden

`implementer.md:8`, rule 2: "No behaviour ships without a test you have seen fail on it" —
the same rule as Law 4 (PLAYBOOK.md:99) — and the steps built on it: Step 3's tests
(implementer.md:38-44) and Step 5's full test-suite run (implementer.md:69-71).

## The fact that contradicts it

This repository has no test suite, no build and no linter
(examples/context/DEPENDENCIES.md:3-4), and records its quality gates as
`none available` (examples/context/DEPENDENCIES.md:37-39). What it ships is text a model
reads; there is no behaviour a test could run, so there is nothing to see fail.

## What applies instead

- **The phase's Verify is the test.** Each `PLAN.md` phase states grep or `fd` commands with
  their expected output. Run them before the edit and see them report the gap, then after it
  and see them come back clean — the same "seen fail" guard, applied to text.
- **A human reads the whole diff before commit.** That is this project's default, not a
  per-task choice (examples/context/README.md:27).
- Everything else in `implementer.md` stands: scope, Step 4.5's judgment items, the
  `Context:` report lines.
