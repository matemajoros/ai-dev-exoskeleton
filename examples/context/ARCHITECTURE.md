# Architecture

This repository is a distributable methodology, not an application: plain-markdown agents,
commands, and guides that a coding agent reads, plus this repo's own copy of the
project-knowledge folder they produce (README.md:1-10, AGENTS.md:3-6).

## Two tiers

- `.ai-dev-exoskeleton/` — universal, project-agnostic: 5 agents, 4 commands, and guides
  (PLAYBOOK, workflows, checklists, `field-notes.md`). Never edited per project
  (AGENTS.md:34-45).
- `docs/` — per-project: `docs/context/` (this project's architecture, patterns, and
  conventions, generated once during onboarding) and `docs/tasks/[yyyymmdd-task-name]/`
  (`CONTEXT.md` / `PLAN.md` / `REVIEW.md` per feature — the session-recovery record)
  (AGENTS.md:46-51).
- The full distributable payload is 20 plain-markdown files: 17 under
  `.ai-dev-exoskeleton/` (verified: `fd -t f . .ai-dev-exoskeleton | wc -l` → 17) plus
  `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` at the repo root (README.md:29).
- `CLAUDE.md` and `GEMINI.md` are thin pointers into `AGENTS.md`, the single canonical
  entry file (CLAUDE.md:3-7, GEMINI.md:3-7).

## The five agents

| Agent | May write | Bound by |
|---|---|---|
| `planner` | Markdown only, in `docs/tasks/[yyyymmdd-task-name]/` | Never edits/creates/modifies source code (planner.md:7-8) |
| `implementer` | Source, tests, config — only files inside the declared SCOPE | Does not refactor beyond the request; notes out-of-scope finds instead of fixing them (implementer.md:10-12) |
| `reviewer` | Only `REVIEW.md` in the current task folder | Never edits source, tests, config, or any project file — reports only (reviewer.md:7-9) |
| `explorer` | Only `docs/context/*.md`, plus the project's entry file during onboarding | Never edits source code, tests, or config (explorer.md:7-9) |
| `debugger` | Code — but only after the root cause is confirmed | Never changes code before completing the trace; a human confirms the analysis first (debugger.md:7,10; README.md:149-150) |

`implementer` is the one agent whose Rules read `MUST` / `do not` rather than a bold
`**NEVER**` — it's the only one actually allowed to touch source (implementer.md:7-12;
contrast planner.md:7, reviewer.md:7, explorer.md:7, debugger.md:7).

## The four commands

- `build-context` — Q&A to align on a feature before planning; writes only `CONTEXT.md`
  (build-context.md:5-8)
- `start-debug` — one-shot root-cause analysis with a fixed output format; never modifies
  code (start-debug.md:3,7-8)
- `review-walkthrough` — walks a list of findings one at a time, waiting for the user to
  say "NEXT" (review-walkthrough.md:3,13)
- `adversarial-review` — an independent, skeptical second opinion, deliberately run in a
  different model/harness than the one that produced the artifact; read-only
  (adversarial-review.md:3-4,16-17,22)

## Artifact flow

```
CONTEXT.md → PLAN.md → (implementation, tracked by git) → REVIEW.md → fix cycle
```

`build-context` writes `docs/tasks/[yyyymmdd-short-description]/CONTEXT.md`
(build-context.md:8,44) → `planner` reads it and writes
`docs/tasks/[yyyymmdd-task-name]/PLAN.md`, phased, with Scope / Depends on / Verify /
Rollback per phase (planner.md:8,33-43,52) → `implementer` executes one phase at a time
inside that phase's SCOPE (implementer.md:4,10) → `reviewer` writes `REVIEW.md` in the same
task folder, findings ranked by severity (reviewer.md:8-10,84-101) → fixes land, then a
human tests the result by hand (AGENTS.md:72-73).

The task-folder slug itself is not consistent across the repo:
`[yyyymmdd-task-name]` (planner.md:8, implementer.md:81, reviewer.md:9),
`[yyyymmdd-short-description]` (build-context.md:8), `[yyyymmdd-refactor-name]`
(refactor.md:11), `[yyyymmdd-name]` (pre-session.md:90,96).

## Where the human is required

Two mandatory gates — the work stops without a human: context building at the start, and
manually exercising the result after review fixes land. Between them, three moments where
an agent brings a decision the human can hand back in a line: the plan, a root-cause
analysis (the debugger blocks on this by design), and the review findings deliberately left
for judgment (README.md:137-154).
