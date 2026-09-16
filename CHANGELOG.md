# Changelog

All notable changes to the AI Dev Exoskeleton are recorded here.
Versioning is informal (this is a methodology, not a package): the version marks a
coherent snapshot you can copy into a repo and expect the docs to match.

## [0.2.0] — 2026-08-21 — honest claims, a worked example

Foundation release: nothing new to learn, four things that were wrong made right.

- **The presence claim is restated to match reality.** `README.md` and `AGENTS.md` used to
  say two human gates were enough. There are two points where your presence is *mandatory*
  — context building, and testing the result yourself — plus three moments where an agent
  brings you a decision: the plan, a root-cause analysis, and the review findings the fix
  session left you. The old claim was not true; a taxonomy that made it come out at two
  would have been worse than the error.
- **`examples/`** — the system now demonstrates itself: `examples/context/` is a filled
  `docs/context/` (this repo describing itself), and
  `examples/task-20260814-onboarding-session5-routing/` is one finished task, reconstructed
  from a real commit and labelled as such.
- **`PLAN.md` gains `## Acceptance`** — observable WHEN → THEN behaviour, never test
  commands. This is the list you walk at the final gate, which until now had nothing to
  check against.
- **`docs/context/` gets an anti-bloat rule.** Update the claim you are replacing rather
  than appending beside it; describe what is true now, not what used to be true; split past
  ~200 lines. A knowledge base that only grows stops being read — by you and by the agent.
- **The second adoption path is documented.** Cloning this repo and starting inside it used
  to hand you every file we own, silently. `README.md` now names that path and lists what to
  delete.
- This repository's own `docs/context/` is a pointer to `examples/context/`, so no adopter
  can inherit our context by copying `docs/` or cloning.

Payload unchanged at 20 files.

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
