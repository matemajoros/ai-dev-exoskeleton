# Project Context — Index

This is the AI Dev Exoskeleton repository describing **itself**, as a worked example of
what a filled `docs/context/` looks like after onboarding. Nothing in this folder is
copied into an adopter's project — it lives under `examples/` precisely so nobody inherits
it by copying `docs/` or cloning this repo (see `docs/context/README.md`).

The table below follows the shape onboarding actually generates
(`.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md:87-109`). The agents in
`.ai-dev-exoskeleton/` are universal; everything specific to a project would live here in a
real adoption.

## Files

| File | Holds | Read it when |
|------|-------|--------------|
| `ARCHITECTURE.md` | The two-tier layout, the five agents and what each may write, the four commands, the artifact flow | planning, reviewing, exploring |
| `PATTERNS.md` | This repo's writing conventions: agent-file skeleton, imperative voice, `NEVER` / `Do NOT`, root-relative paths | implementing, reviewing |
| `DATA_MODEL.md` | **Skipped.** No database, no entities, no schema — see below | — |
| `API_SURFACE.md` | **Skipped.** No REST/GraphQL/CLI surface — see below | — |
| `DEPENDENCIES.md` | Honestly short: no runtime, no manifest; which harnesses are assumed, what `@path` expansion needs | onboarding, setup |

On a small repo, reading all of these is cheap — do that. On a large repo, scope down to
what the task needs. Every claim cites a source (`file:line`).

Keep these current, not cumulative. Before adding a claim, find the claim it replaces or
contradicts and update that one — a file that only ever grows stops being read, by you and
by the agent. Describe what is true now, never what used to be true; history lives in git
and in `docs/tasks/archive/`. If a file passes ~200 lines, split it by domain
(`PATTERNS-api.md`, `PATTERNS-frontend.md`) and update this index.

## Why two files are missing, not stubbed

The five-file menu the explorer offers during onboarding
(`.ai-dev-exoskeleton/agents/explorer.md:42-46`) is a **menu, not a checklist.** This
repository is markdown files an agent reads — no database, no schema, no entities to
relate, and no REST/GraphQL/CLI surface to document. Writing `DATA_MODEL.md` or
`API_SURFACE.md` just to hold the sentence "not applicable" would be the exact ritual this
system exists to avoid. Recording the skip here, instead, is the legitimate outcome — an
adopter should feel equally free to omit a category that genuinely doesn't apply to their
project, rather than pad it out to complete the set.
