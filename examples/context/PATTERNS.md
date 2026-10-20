# Patterns

This repo's content is prose, not code — its "patterns" are the writing conventions its own
agent and command files follow. Discovered by reading them, not assumed.

## Agent-file skeleton

Every file in `.ai-dev-exoskeleton/agents/` opens the same way: title (`# Agent: Name`) →
one-line mission as a blockquote → `## Rules` (numbered) → `## Project knowledge` →
`## Process` — e.g. planner.md:1-22, debugger.md:1-20, implementer.md:1-23. Process uses
`### Step N` sub-headings everywhere except `explorer`, whose Process is keyed by question
type (explorer.md:22, explorer.md:28, explorer.md:33, explorer.md:39).

After `## Process` the five files diverge into two shapes:

- `planner`, `implementer`, `debugger` have `## Anti-Patterns to Avoid` (planner.md:98,
  implementer.md:93, debugger.md:50); their output template is a fenced block embedded inside
  a Process step rather than its own section (planner.md:55-96, implementer.md:25-31,
  debugger.md:36-41). `debugger` follows its Anti-Patterns with two situational sections
  (debugger.md:57, debugger.md:79).
- `explorer` and `reviewer` instead have a dedicated `## Output Format` section holding the
  fenced template (explorer.md:49-64, reviewer.md:74-103); neither has an Anti-Patterns
  section. `reviewer` adds one further section after it, `## Feedback Loop`
  (reviewer.md:105-109).

Whatever the shape, all nine agent and command files end on the same line: "If
`docs/context/overrides/<this file's name>` exists, read it — where it conflicts with this
file, it wins." (planner.md:102, implementer.md:99, reviewer.md:112, explorer.md:66,
debugger.md:86, build-context.md:86, start-debug.md:44, review-walkthrough.md:15,
adversarial-review.md:58). It is always the file's last line, set off by a blank line.

The two `references/` files are a lighter skeleton: `# Reference: Name` → a blockquote saying
when to read the file (code-quality.md:1-4, heavy-mode.md:1-3), and no override line.

## Imperative, second-person voice

Rules read as direct commands, not descriptions. Four of the five agent files state their
absolute constraint with a bold `**NEVER**` (planner.md:7, reviewer.md:7, explorer.md:7,
debugger.md:7). `implementer.md` is the exception — the one agent actually allowed to touch
source — so its Rules read `MUST` / `do not` instead (implementer.md:7-12).

`Do NOT` (capitalized, not bolded) carries narrower guidance: the Anti-Patterns bullets
(planner.md:99-100, implementer.md:94-97, debugger.md:51-55) and a command's hard stops
(build-context.md:44, build-context.md:84). No command's "Quick Rules" section uses it;
those are written as `NEVER` / `ONLY` (build-context.md:6-7, start-debug.md:8-10).

Second person appears explicitly when a rule has to scope itself to the agent's own output:
"code YOU wrote or changed in this session" (implementer.md:52).

## Root-relative paths

Cross-references in agent and command files are written from the repo root —
`docs/context/README.md` (explorer.md:17), `.ai-dev-exoskeleton/references/heavy-mode.md`
(implementer.md:19) — never a relative `../` path. The one exception found:
`start-debug.md:5` points to `../agents/debugger.md`.

## Fenced output templates

Any file that hands off a document a later session will read defines its exact shape as a
fenced code block: `PLAN.md` (planner.md:55-96), `REVIEW.md` (reviewer.md:75-103),
`CONTEXT.md` (build-context.md:50-78), the implementer's DONE report
(implementer.md:81-87), the debug root-cause trace (start-debug.md:23-27), the explorer's
answer format (explorer.md:49-64), the adversarial review (adversarial-review.md:41-56).
The override line always sits after the template, outside the fence (reviewer.md:112,
explorer.md:66, adversarial-review.md:58).

## The MODE / SCOPE / CONSTRAINT / DONE WHEN block

Defined once, as the optional prompt scaffold under `## Prompt scaffold (optional)` —
"Use it when a session keeps drifting; skip it if you already write tight prompts"
(AGENTS.md:19-28). README.md:44-52 shows the same four fields verbatim, and PLAYBOOK's
`### Prompt Scaffold (optional)` repeats them, naming `CONTEXT:` and `ERROR:` as additions
(PLAYBOOK.md:180-193). Workflow guides reuse it as a copy-paste session opener rather than
re-describing it: feature.md:45-55, debug.md:6-15, refactor.md:6-21. The pre-session
quick-start templates borrow single fields inside prose prompts instead
(pre-session.md:85, pre-session.md:100-101).
