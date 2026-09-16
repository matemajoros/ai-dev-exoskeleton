# Patterns

This repo's content is prose, not code — its "patterns" are the writing conventions its own
agent and command files follow. Discovered by reading them, not assumed.

## Agent-file skeleton

Every file in `.ai-dev-exoskeleton/agents/` opens the same way: title (`# Agent: Name`) →
one-line mission as a blockquote → `## Rules` (numbered) → `## Project knowledge` →
`## Process` (`### Step N` sub-headings) — e.g. planner.md:1-20, debugger.md:1-20,
implementer.md:1-22.

After `## Process` the five files diverge into two shapes:

- `planner`, `implementer`, `debugger` close with `## Anti-Patterns to Avoid`
  (planner.md:96, implementer.md:94, debugger.md:61); their output template is a fenced
  block embedded inside a Process step rather than its own section (planner.md:52-94,
  implementer.md:26-31, debugger.md:29-32).
- `explorer` and `reviewer` instead close with a dedicated `## Output Format` section
  holding the fenced template (explorer.md:50-66, reviewer.md:83-101); neither has an
  Anti-Patterns section. `reviewer` adds one further section after it, `## Feedback Loop`
  (reviewer.md:103-107).

## Imperative, second-person voice

Rules read as direct commands, not descriptions. Four of the five agent files state their
absolute constraint with a bold `**NEVER**` (planner.md:7, reviewer.md:7, explorer.md:7,
debugger.md:7). `implementer.md` is the exception — the one agent actually allowed to touch
source — so its Rules read `MUST` / `do not` instead (implementer.md:7-12).

`Do NOT` (capitalized, not bolded) is reserved for narrower, example-level guidance inside
`## Anti-Patterns to Avoid` and command "Quick Rules" sections — e.g. planner.md:97-100,
implementer.md:95-100, debugger.md:62-66, build-context.md:83-87.

Second person appears explicitly when a rule has to scope itself to the agent's own output:
"code YOU wrote or changed in this session" (implementer.md:50).

## Root-relative paths

Cross-references are written from the repo root — `docs/context/README.md`
(implementer.md:15), `.ai-dev-exoskeleton/agents/planner.md` (AGENTS.md:36) — never a
relative `../` path. The one exception found: `start-debug.md:5` points to
`../agents/debugger.md`.

## Fenced output templates

Any file that hands off a document a later session will read defines its exact shape as a
fenced code block: `PLAN.md` (planner.md:52-94), `REVIEW.md` (reviewer.md:84-101),
`CONTEXT.md` (build-context.md:46-69), the debug root-cause trace (start-debug.md:26-30),
the explorer's answer format (explorer.md:51-66).

## The MODE / SCOPE / CONSTRAINT / DONE WHEN block

Defined once, canonically, as "The one rule" (AGENTS.md:23-28), and restated verbatim in
README.md:47-52 and as the "Prompt Structure" in PLAYBOOK.md:155-161. Every workflow guide
reuses it as a copy-paste session opener rather than re-describing it: feature.md:44-54,
debug.md:6-15, refactor.md:6-21, pre-session.md:78-109.
