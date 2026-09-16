# Dependencies

Short by design: this repo has no runtime, no package manifest, no build, and no test suite
of its own — it is 20 markdown files a coding agent reads (README.md:8-10, AGENTS.md:4-6).
Confirmed by directory listing: no `package.json`, `requirements.txt`, `pyproject.toml`,
`Makefile`, `Dockerfile`, `Gemfile`, or `go.mod` anywhere in the repo.

## What's actually here

- Plain markdown: agents, commands, and guides under `.ai-dev-exoskeleton/`; the entry
  files `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`; project docs under `docs/`.
- `VERSION` (currently `0.1.0`) and `CHANGELOG.md`, tracking the methodology's own
  snapshots. Versioning is informal, because "this is a methodology, not a package"
  (CHANGELOG.md:4-5).
- `.gitignore` excludes editor/OS junk, `.env*`, logs, and `node_modules/` — the last one
  is there "only relevant if you add tooling" (`.gitignore`), i.e. the exoskeleton itself
  never generates any.

## What it assumes

Actually run under: Claude Code, Gemini CLI, ChatGPT Codex, OpenCode (with MiniMax), and
KiloCode (with MiniMax) — no porting needed, because plain markdown referenced by path
works the same in all of them (README.md:108-109).

`@path` expansion: in Claude Code and Gemini CLI, writing
`@.ai-dev-exoskeleton/agents/planner.md` auto-expands the file into context; in other
harnesses the agent is just asked to open the path (AGENTS.md:38-39, README.md:110-111).

## What you need installed

Nothing. There is no install step (README.md:8). The only prerequisite is a coding
agent/harness that can read a file by path — everything else in this system is the text
itself.
