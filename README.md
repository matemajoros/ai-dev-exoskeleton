# AI Dev Exoskeleton

A minimal, project- and LLM-agnostic system for **disciplined agentic engineering** —
a set of plain-markdown agents, commands, and guides you drop into any repo and fill
with project context in 20–90 minutes, then develop fast even on a codebase you've
never seen.

No runtime. No dependencies. No install. The files are text a coding agent reads;
they happen to contain behavioral instructions. That is the whole trick — and the
reason it runs unchanged across harnesses and models.

**This is the system I hand to development teams when I run adoption workshops.** It's
published so anyone can see exactly what those teams adopted — and it is deliberately
small, because a system a normal team actually keeps using beats a powerful one they
abandon.

---

## Who has actually used this

- A **~300-person software company**. I presented the method to the person responsible
  for their AI transition, then ran a workshop for all their tech leads, then further
  workshops for several dev teams. I handed over the files and the methodology for free.
  Since then, AI-assisted development following this method has become their default on
  most of their projects.
- A **large construction firm** (hundreds of employees, ~10-person IT department). Same
  workshop, same handover. They took it into their day-to-day work too. This one matters
  most to me: it is not a software company, and a small IT team adopted it anyway —
  because it was 20 files of plain markdown, not a platform.
- **An intern I taught.** Roughly 4× the throughput he had before, while simultaneously
  getting through all his university exams — 4–5 features shipped in the same window.

Both companies reported the same two things: faster delivery, and noticeably more
thorough code review.

## What this is

An **exoskeleton**: it amplifies a developer instead of replacing them. Every step is
constraint-driven and evidence-based, and a human stays the decision-maker at the gates
that matter — chiefly at the start, where the work gets its direction, and at the end,
where you check whether it actually works. The agent plans, implements, and reviews; you
hold the line on scope, correctness, and "done."

Writing a sharp, focused prompt is a skill, and most vague results come from a vague ask.
These keywords are a scaffold for it — use them if you feel the AI usually does other things than you asked for:

```
MODE:       plan | implement | review | debug | explore
SCOPE:      which files/dirs are in play (everything else is off-limits)
CONSTRAINT: what NOT to do (don't refactor, don't touch the API, no code yet)
DONE WHEN:  the specific exit condition
```

Work flows through small, testable sessions:

```
build-context  →  plan  →  implement (tested)  →  review  →  fix  →  test it yourself
   align on        phased    one phase per          report     targeted   you exercise
   the feature     plan      session, tests pass    findings   fixes      the result
   ▲                                                                      ▲
   └─────────────────── your two mandatory checkpoints ───────────────────┘
```

Each stage is a universal role in `.ai-dev-exoskeleton/agents/`
(`planner` · `implementer` · `reviewer` · `explorer` · `debugger`). They never change
between projects. Everything project-specific lives in `docs/context/`, generated once
during onboarding.

### Why not just use your harness's built-ins?

Fair question. Claude Code has plan mode, subagents, and memory files; other harnesses
have their own equivalents, and they're good. Two reasons this exists anyway:

- **They don't survive a harness switch.** Every native feature is a different shape in a
  different tool. Plain markdown referenced by path is the lowest common denominator that
  works in all of them — that portability *is* the design, not a limitation of it.
- **Native features are capabilities, not a practice.** Plan mode doesn't tell you how to
  size a session against your context window, or that a phase needs an explicit file scope
  and a rollback. This is the process layer; use it on top of whatever your harness gives you.

If you're a power user happy inside one harness, tools like Superpowers or GSD will give
you more. This is aimed at the other case: getting a whole team to work this way, in
whatever tool each of them uses.

## How to use it

1. **Get the files onto disk, one of two ways:**
   - **Copy into your repo's root:** the `.ai-dev-exoskeleton/` folder, `AGENTS.md`, and
     `CLAUDE.md` / `GEMINI.md` if you use those harnesses. All four are generic — nothing in
     them is specific to this repo. (Don't copy `docs/` — that's this repo's own project
     knowledge; onboarding writes yours.)
   - **Clone this repository and start your project inside it.** You inherit every file we
     own, so delete them first: `docs/`, `examples/`, `CHANGELOG.md`, `.github/`, and replace
     `LICENSE` and `README.md` with your own. Keep `.ai-dev-exoskeleton/`, `AGENTS.md`, and
     `CLAUDE.md` / `GEMINI.md` — the same files the copy path uses.

   That install payload — `.ai-dev-exoskeleton/` plus `AGENTS.md`, `CLAUDE.md` and
   `GEMINI.md` — stays at or under 30 files, and is 23 today. `docs/context/` (generated per
   project), `examples/`, and this repository's `README.md`, `CHANGELOG.md`, `LICENSE` and
   `.github/` are never copied, so they don't count.
2. **Run onboarding** (`.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md`) —
   the agent explores the codebase and writes `docs/context/` (architecture, patterns,
   conventions, gotchas) plus its index, and fills in the repo entry file.
   **20–90 minutes**, depending on repo size.
3. **Work** through the feature / debug / refactor workflows in
   `.ai-dev-exoskeleton/guides/workflows/`.

Start at **[AGENTS.md](AGENTS.md)** — the canonical guide the coding agent reads.
`CLAUDE.md` and `GEMINI.md` are thin pointers to it, so each harness auto-discovers the
system from a single source of truth.

**Harness- and model-agnostic — actually run under:** Claude Code, Gemini CLI, ChatGPT
Codex, OpenCode (with MiniMax), and KiloCode (with MiniMax). Because it's plain markdown
referenced by path, there is nothing to port. (In Claude Code and Gemini CLI `@path`
auto-expands; elsewhere the agent just opens the path.)

## When I don't recommend using it

Two cases where I'd tell you not to bother:

- **You've already mastered another methodology or harness, and you lean on its framework
  and default features.** If that's working for you, you don't need another small
  methodology layered on top. The value here is having *a* deliberate process that travels
  between tools — not this particular one being uniquely right. Someone who already has one
  gains little.
- **You have no domain knowledge and no way to get it.** Everything in this system exists
  to move good context from your head into the agent's — `build-context` before planning,
  `docs/context/` for the codebase, an explicit scope per phase. If you can't supply that
  context, no amount of process will manufacture it. The method amplifies what you know; it
  doesn't substitute for knowing.

## Honest about enforcement

Every constraint here — "the reviewer never edits," "stay in scope," "trace before you
touch" — is a **convention the agent is asked to follow, not a sandbox that enforces it.**
Models violate instructions. The discipline lives in the human holding the gates: if you
approve the agent's work without actually reading it, that discipline is gone and you get
the model's raw, unassisted quality. This system makes the right process easy and legible —
it does not make it automatic.

**Where you are actually needed.** Two points where your presence is mandatory — the work
stops without you:

1. **Context building** — the highest-leverage moment in the loop, and the one thing you
   cannot delegate.
2. **A manual test after the review fixes land** — you, exercising the actual thing, before
   it is called done.

Between them the work runs without you, with four moments where an agent brings you a
decision:

- **The plan**, before implementation starts — this is where mistakes are still free.
- **A root-cause analysis**, before any debugging fix is applied. The debugger blocks here
  by design: it will not touch code until you confirm.
- **The review findings the fix session left you** — the design trade-offs and ambiguous
  requirements it deliberately declined to decide on your behalf.
- **A new test seam**, when the implementer declares one — it proceeds without waiting; a
  line from you stops it.

You can hand any of those four back in a line. You cannot hand back the two gates.

## Where the method came from, and what I can and can't prove

The playbook's laws are distilled from a message-level analysis of **hundreds of my own
agentic-engineering sessions**, out of roughly 300+ hours of hands-on
use.

### On speed — read the caveats first

I'll state the limits before the numbers, because the limits are the more useful part.

**This is not a controlled experiment, and I can't make it one.** What I have is a
working developer's baseline: the same people, comparable projects, different points in
time. That means at least three confounders I cannot separate out:

- **The models got dramatically better** over the same period. Some unknown share of any
  speedup is the model improving, not the method.
- **Project-to-project variation** in scope, familiarity, and stack is large.
- **Selection.** The best result is the best result — it is the tail of a distribution,
  not the middle of one.

With that said, here is what I actually have:

- **On some projects: a large speedup, which I measured.** I tracked every worked hour in
  Toggl, then compared the total against our own delivery hours on previous projects of
  comparable scope and complexity. On the best-fit project that comparison came out around
  12×. Treat that as "what happened once, on favourable ground," not as a number to expect —
  and see the confounders above before you believe any of it is purely the method.
- **On typical feature work: roughly 2-4×.** This one is an honest
  estimate, not a tracked number. The mechanism is mundane: I run 4–5 agents in parallel
  across git worktrees, so I cover more ground than working one task at a time alone.

What I'd rather be judged on is the first section of this README: two organisations put
this into daily practice after a workshop, and one of them isn't a software company.
That's verifiable by asking them, which is more than any multiplier of mine is worth.

## License & contributing

MIT — see [LICENSE](LICENSE). Already given away freely; use it, fork it, make it yours.

Issues welcome, especially **"I tried this and here's where it broke"** — that's the most
useful signal there is. No roadmap and no support commitment: this is a working artifact I
use daily and hand to teams, published so others can too.
