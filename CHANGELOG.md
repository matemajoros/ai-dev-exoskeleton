# Changelog

All notable changes to the AI Dev Exoskeleton are recorded here.
Versioning is informal (this is a methodology, not a package): the version marks a
coherent snapshot you can copy into a repo and expect the docs to match.

## Upgrading a copied exoskeleton

This system is copied into each repo, so copies drift from the source. Check
`.ai-dev-exoskeleton/VERSION` to see which release a project has (no file means 0.2.0 or
older). To upgrade, replace its `.ai-dev-exoskeleton/` folder with the new version, re-check
the repo's `AGENTS.md` pointer, and follow the migration note of every release in between.
Your `docs/context/` (project knowledge) is untouched.

## [0.3.0] — 2026-09-16 — rigor you choose, tests that prove something

Rigor becomes a choice you make per task, and what an agent needs only sometimes moves out
of the files every session loads.

- **Rigor is one switch: `light | heavy`.** `build-context` ends by asking *"Would you have
  asked another human to review this change?"* and records the answer in `CONTEXT.md`; the
  project's default lives in the `docs/context/` index. You pick — an agent may argue for
  heavier, never for lighter. Light allows a one-phase plan; heavy adds a plan review,
  `adversarial-review`, a gate loop, and a final hardening phase in the plan. Still seven
  workflow steps. See PLAYBOOK, "Light or heavy".
- **Tests are judged by value, not order.** The ordering rule is replaced by: no behaviour
  ships without a test you have seen fail on it. The implementer names its `SEAM:` up front;
  a new seam is a fourth decision point, declared without waiting — a line from you stops it.
  Tautological tests and horizontal slicing are banned, tests sit at the highest level the
  project can run, and `## Acceptance` items are written so they can be executed.
- **Review checks intent first.** `REVIEW.md` opens with a met / not met / partial ruling on
  every acceptance item and ends with pasted command output and a low / medium / high risk
  line. Low risk with real evidence is the one case where you may skip reading the diff; the
  result is still yours.
- **The knowledge base knows what changed.** The implementer reports each `docs/context/`
  edit as added, modified or removed, with `file:line`. Onboarding records the project's
  quality gates ("none available" is a valid answer) and asks for a default rigor.
- **Overrides without forking.** Each agent and command ends with one line: a matching file
  in `docs/context/overrides/` wins. PLAYBOOK's "Adapting a rule without forking" says what
  belongs there and states the layer's open risks. Onboarding may propose at most three,
  inert until you rename them.
- **`references/` holds what is read only when a condition matches.** The two copies of the
  numeric quality checklist are now one file, opened only when no gate is recorded;
  heavy-only rules live in `heavy-mode.md`.
- **Law 1 asks whether the artifacts are current enough to end the session**, not how full
  the window is. Its symptom list stays.
- **`VERSION` moved into `.ai-dev-exoskeleton/`**, so a copied exoskeleton says what it is.
  `README.md` states the ≤30-file budget and how files are counted.
- **Consistency fixes.** One task-folder slug, `[yyyymmdd-task-name]`. One severity scale,
  CRITICAL / WARNING / NOTE, in `adversarial-review` too. MODE / SCOPE / CONSTRAINT / DONE
  WHEN is an optional prompt scaffold, not a mandatory rule. Nothing points at an archive
  folder no command creates: history lives in git.
- **The 0.1.0 entry's hours and session figures were removed.** They contradicted
  `README.md`, which is now the only place they are stated.
- **The planner gained two design principles, and only the two that earned it.** Three planner
  runs on the same feature — two without a draft of borrowed principles, one with it — showed
  that the deletion test and the one-word-per-concept rule change a plan, while
  "one adapter is a hypothetical seam" changed nothing on prose work. Only the first two
  shipped on that evidence, into `planner.md` Step 3. After Ousterhout and Pocock.
- **When to abstract is answered by reversibility, not by prediction.** A third planner line,
  and one reviewer line, come from practice rather than that test: one implementation is a
  hypothetical seam, so call the concrete code until a second exists — unless the decision
  leaks outward (public API, schema, wire or file format, a module others import, anything
  needing a migration), where someone you can't edit writes the second case. The reviewer's
  half is pointed the other way too: don't ask for generality without naming a second case
  that exists today.

**Migrating from 0.2.0.** Replace the folder; re-home anything you had edited inside the old one
by PLAYBOOK's `## Adapting a rule without forking` table (`overrides/` is its rare row). Replace
`CLAUDE.md` / `GEMINI.md`, and merge the new generic top of `AGENTS.md` above your project's own
sections. Re-run onboarding Session 3 (quality gates) and Session 4 (override proposals). Add `**Default rigor:** light | heavy — [why, for this project as a whole]` to your
`docs/context/README.md`. Output formats changed: `CONTEXT.md` gained `## Rigor` (a task already in flight has none, which reads as light); `REVIEW.md` gained
`### Acceptance`, `### Evidence` and `### Risk`; the implementer's Step 1 block gained `SEAM:`
and its DONE block `- Context:` lines.

Payload: 23 files. Agents and commands: 668 lines, matching 0.2.0's 668. All of
`.ai-dev-exoskeleton/`: 1,835 lines, up from 1,642 — the two `references/` files, onboarding's
gates and override steps, and PLAYBOOK's two new sections.

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

Initial public version, distilled from the author's own agentic-engineering sessions (the
figures are in `README.md`) and refined through workshops at two companies.

- **Agents** (universal roles): planner, implementer, reviewer, explorer, debugger.
- **Commands**: build-context, start-debug, review-walkthrough, adversarial-review.
- **Guides**: PLAYBOOK (the Laws), workflows (feature, debug, refactor, onboarding),
  pre/post-session checklists, field-notes.
- **Project knowledge** lives in `docs/context/`; the exoskeleton itself stays universal.
- Harness adapters: canonical `AGENTS.md` with `CLAUDE.md` / `GEMINI.md` pointers.
