# Architecture

This repository is a distributable methodology, not an application: plain-markdown agents,
commands, and guides that a coding agent reads, plus this repo's own copy of the
project-knowledge folder they produce (README.md:1-10, AGENTS.md:3-6).

## Two tiers

- `.ai-dev-exoskeleton/` — universal, project-agnostic: 5 agents, 4 commands, 2 references,
  guides (PLAYBOOK, workflows, checklists, `field-notes.md`), and `VERSION`. Never edited
  per project (AGENTS.md:34-49). A reference opens only on its own condition:
  `code-quality.md` when `DEPENDENCIES.md` records no lint or complexity gate — a lone
  coverage gate does not switch it off (code-quality.md:3); `heavy-mode.md` when the task
  is heavy (heavy-mode.md:3).
- `docs/` — per-project: `docs/context/` (this project's architecture, patterns,
  and conventions, generated once during onboarding, with `overrides/` for a method rule that
  can't hold here) and `docs/tasks/[yyyymmdd-task-name]/` (`CONTEXT.md` / `PLAN.md` /
  `REVIEW.md` per feature — the session-recovery record) (AGENTS.md:50-55).
- The install payload is 23 files: 20 under `.ai-dev-exoskeleton/` — 5 agents, 4 commands,
  2 references, 8 guides, and `VERSION` (verified: `fd -H -t f . .ai-dev-exoskeleton | wc -l`
  → 20) — plus `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` at the repo root. It stays at or under
  30 files (README.md:97-100).
- `CLAUDE.md` and `GEMINI.md` are thin pointers into `AGENTS.md`, the single canonical
  entry file (CLAUDE.md:3-8, GEMINI.md:3-8).

## The five agents

| Agent | May write | Bound by |
|---|---|---|
| `planner` | Markdown only, in `docs/tasks/[yyyymmdd-task-name]/` | Never edits/creates/modifies source code (planner.md:7-8) |
| `implementer` | Source, tests, config — only files inside the declared SCOPE | Does not refactor beyond the request; notes out-of-scope finds instead of fixing them (implementer.md:10-12) |
| `reviewer` | Only `REVIEW.md` in the current task folder | Never edits source, tests, config, or any project file — reports only (reviewer.md:7-9); rules every acceptance item met / not met / partial before it verifies anything (reviewer.md:24-27) |
| `explorer` | Only `docs/context/` files, `overrides/` included, plus the project's entry file during onboarding | Never edits source code, tests, or config (explorer.md:7-9) |
| `debugger` | Code — but only after the root cause is confirmed | Never changes code before completing the trace; a human confirms the analysis first (debugger.md:7, debugger.md:10, README.md:153-154) |

`implementer` is the one agent whose Rules read `MUST` / `do not` rather than a bold
`**NEVER**` — it's the only one actually allowed to touch source (implementer.md:7-12;
contrast planner.md:7, reviewer.md:7, explorer.md:7, debugger.md:7).

## The four commands

- `build-context` — asks its clarifying questions, the task's rigor last,
  and writes only `CONTEXT.md` (build-context.md:26-37, build-context.md:6-7)
- `start-debug` — one-shot root-cause analysis with a fixed output format; never modifies
  code (start-debug.md:3, start-debug.md:8)
- `review-walkthrough` — walks a list of findings one at a time, waiting for the user to
  say "NEXT" (review-walkthrough.md:3, review-walkthrough.md:13)
- `adversarial-review` — an independent, skeptical second opinion, deliberately run in a
  different model/harness than the one that produced the artifact; read-only, findings
  ranked CRITICAL > WARNING > NOTE (adversarial-review.md:3-4, adversarial-review.md:16-17,
  adversarial-review.md:22-23)

## Artifact flow

```
CONTEXT.md → PLAN.md → (implementation, tracked by git) → REVIEW.md → fix cycle → manual test
```

`build-context` writes `docs/tasks/[yyyymmdd-task-name]/CONTEXT.md`, ending with
`## Rigor` (build-context.md:37, build-context.md:73-74) → `planner` reads it and writes
`PLAN.md` in the same folder, phased, with Scope / Depends on / Verify / Rollback per phase;
`light` allows a single phase (planner.md:15, planner.md:28-44, planner.md:54) →
`implementer` executes one phase at a time inside that phase's SCOPE, declaring its `SEAM:`
first (implementer.md:10, implementer.md:25-33); a heavy plan ends with a hardening phase it
executes like any other (heavy-mode.md:10-14, feature.md:111-113) →
`reviewer` rules each `## Acceptance` item, then
writes `REVIEW.md`: findings by severity, pasted evidence, and a Risk line
(reviewer.md:24-27, reviewer.md:75-103) → fixes land, then a human walks `## Acceptance` by
hand, reading the reviewed diff unless the risk is low with evidence — and reading whatever
the fix session changed either way, since nobody rated that (feature.md:149-156,
AGENTS.md:76-77).

One slug names every task folder, `[yyyymmdd-task-name]` (AGENTS.md:54, planner.md:8,
build-context.md:7, reviewer.md:9).

## Where the human is required

Two mandatory gates — the work stops without a human: context building at the start, and
manually exercising the result after review fixes land. Between them, four moments where
an agent brings a decision the human can hand back in a line: the plan, a root-cause
analysis (the debugger blocks on this by design), the review findings deliberately left
for judgment, and a new test seam — the implementer declares it and proceeds without
waiting; a line from the human stops it (README.md:141-160, AGENTS.md:8-14).
