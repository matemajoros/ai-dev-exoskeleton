# Workflow: New Project Onboarding

> How to set up your agentic engineering system when you join a new project.
> Goal: Go from zero to productive in 20-90 minutes.

## What You Bring (no changes needed)

Your `.ai-dev-exoskeleton/agents/*.md` files are universal — they work on any project, any language, any stack.
Your `.ai-dev-exoskeleton/guides/workflows/*.md` and `.ai-dev-exoskeleton/guides/checklists/*.md` are also universal.

## What You Rebuild (project-specific)

- `docs/context/` — structured architecture, patterns, and gotchas for this codebase.
  **This is the entire per-project fill-in** — everything the agents need to know
  about THIS project lives here, and the universal agents read it by pointer.
- `AGENTS.md` (and the `CLAUDE.md` / `GEMINI.md` pointers) — the repo entry file
- `docs/tasks/` — task folders for plans, notes, and work artifacts

---

## Session 1: Set Up the Exoskeleton
```
From the ai-dev-exoskeleton repository, copy into the root of your project repository:
  1. the .ai-dev-exoskeleton/ folder (the universal system)
  2. AGENTS.md (describes the system and the one rule — generic, nothing repo-specific)
  3. CLAUDE.md and/or GEMINI.md if you use those harnesses (thin pointers to AGENTS.md)

Do NOT copy docs/ — that is the exoskeleton repo's own project knowledge. Session 2
writes yours, and extends AGENTS.md with this project's specifics.
```

## Session 2: Explore & Generate Project Context (20-30 min)

```
MODE: explore
SCOPE: the entire repo root
CONTEXT: I'm new to this project. I don't know the codebase.
  Explore the codebase, then produce structured documentation.
CONSTRAINT: Do NOT change any source code. Only read, report, and create
  the output files below.
DONE WHEN: The following files are created:

  1. docs/context/ARCHITECTURE.md — high-level architecture map containing:
     - Directory structure and what each top-level dir does
     - Architecture pattern (monolith, microservices, hexagonal, MVC, etc.)
     - Module boundaries and dependency flow between layers
     - Entry points (main files, API routes, CLI commands)
     - Service boundaries and communication methods
     - Deploy process (CI/CD, environments)
     - ASCII diagram of the architecture if useful

  2. docs/context/PATTERNS.md — coding conventions and patterns:
     - Code style conventions (tabs/spaces, formatting, linting)
     - Naming conventions (files, classes, functions, variables)
     - Import/module patterns
     - How services/components are structured
     - Exception/error handling patterns
     - DTO/data transfer patterns
     - Test patterns and test framework usage

  3. docs/context/DATA_MODEL.md — data layer documentation:
     - Key entities and their relationships
     - Database/schema overview
     - ORM/data access patterns used
     - Migration approach (if applicable)
     - Data flow across service boundaries

  4. docs/context/API_SURFACE.md — interface documentation:
     - REST/GraphQL/gRPC endpoints and their purpose
     - CLI commands (if applicable)
     - Request/response patterns
     - Authentication/authorization approach
     - External API integrations

  5. docs/context/DEPENDENCIES.md — dependency and config documentation:
     - Tech stack (languages, frameworks, databases, infra) with versions
     - Key external dependencies and what they're used for
     - Key config files and their purpose
     - Environment variables
     - How to run the app locally (dev commands)
     - How to run tests (test commands, test framework)

  6. docs/context/README.md — the index every agent starts from. One table row per
     context file: what it holds, and when to read it. Every agent is instructed to
     read this index first, so it MUST exist. Template:

     ```markdown
     # Project Context — Index

     Project-specific knowledge for this codebase. The agents in
     `.ai-dev-exoskeleton/` are universal; everything specific to THIS project is here.

     | File | Holds | Read it when |
     |------|-------|--------------|
     | `ARCHITECTURE.md` | [one line] | planning, reviewing, cross-service debugging |
     | `PATTERNS.md` | [one line] | implementing, reviewing |
     | `DATA_MODEL.md` | [one line] | planning, data-layer work |
     | `API_SURFACE.md` | [one line] | API work, integration debugging |
     | `DEPENDENCIES.md` | [one line] | onboarding, debugging, setup |

     On a small repo, reading all of these is cheap — do that. On a large repo, scope
     down to what the task needs. Every claim cites a source (`file:line`).
     ```

  7. AGENTS.md — EXTEND the AGENTS.md already in the repo root (copied in Session 1).
     Keep everything that's there — it describes the system and the one rule, and is
     the single source of truth for that. Retitle the top line to `# Project: [Name]`
     and APPEND the project-specific sections below:

     ```markdown
     ## Quick Overview
     [2-3 sentences about what the project does]

     ## Tech Stack
     - [Language] [version], [Framework] [version]
     - [Database], [ORM/data layer]
     - [Other key technologies]

     ## Build & Run
     [commands to build and run the project locally]

     ## Test Commands
     # Unit tests
     [command]

     # Integration tests (prerequisites: [list any needed services])
     [command]

     # Single test file
     [command]

     ## Project Structure
     See docs/context/ARCHITECTURE.md for detailed architecture.

     ## Coding Conventions
     See docs/context/PATTERNS.md for patterns and conventions.

     ## Key Files
     - [path] — [brief description]
     - [path] — [brief description]

     ## Environment Variables
     - [VAR_NAME] — [purpose]

     ## Important Context
     - docs/context/ARCHITECTURE.md
     - docs/context/PATTERNS.md
     - docs/context/DATA_MODEL.md
     - docs/context/API_SURFACE.md
     - docs/context/DEPENDENCIES.md

     ## Common Gotchas
     - [gotcha discovered during explore]

     ## Rules
     - Always follow existing patterns — check similar code before creating new
     - [project-specific rules]
     ```

Use @.ai-dev-exoskeleton/agents/explorer.md
```

`AGENTS.md` is the canonical entry file. Add thin `CLAUDE.md` and `GEMINI.md` pointers
(each just says "read @AGENTS.md") so Claude Code and Gemini CLI auto-discover it from a
single source of truth.

## Session 3: Establish Feedback Loop (10-15 min)

The agent can only verify its own work if it can run tests. This session ensures
the test feedback loop works before you start real tasks.

```
MODE: explore
SCOPE: the entire repo root
CONTEXT: I need to verify that all test suites run from the command line.
  Try running unit tests, integration tests, and any other test suites
  you can find. Document what works and what doesn't.
CONSTRAINT: Do NOT change any source code. Only run tests, diagnose
  blockers, and update documentation.
DONE WHEN: The following are confirmed and documented in AGENTS.md:

  1. Unit tests — working CLI command that runs unit tests
  2. Integration tests — working CLI command (if they exist), plus any
     prerequisites (Docker containers, env vars, test databases, etc.)
  3. E2E tests — working CLI command (if they exist)
  4. Any blockers — tests that fail, missing dependencies, environment
     issues that need manual setup

  If any test suite cannot run without manual intervention, document
  what's needed so we can fix it.

Use @.ai-dev-exoskeleton/agents/explorer.md
```

### If tests don't run cleanly
Fix environment issues in a follow-up implementation session before proceeding:

```
MODE: implement
SCOPE: test configuration, docker-compose, CI config
CONTEXT: Test suite doesn't run cleanly. Fix the blockers identified
  in the previous session.
CONSTRAINT: Only fix test infrastructure — do not change application code.
DONE WHEN: Test commands documented in AGENTS.md run successfully.
```

### Optional: E2E verification for UI projects
If the project has a frontend, consider setting up E2E verification. Choose
the technique that fits your stack:

- **Playwright** — browser automation, good for complex UI flows
- **Chrome MCP / browser tools** — lightweight, good for visual verification
- **API-level testing** — if the UI is thin, test the API directly
- **Screenshot comparison** — for visual regression testing

Document the chosen approach and commands in AGENTS.md.

## Session 4: Sharpen Conventions & Gotchas (15-20 min)

Session 2 produced `docs/context/`. This session sharpens `PATTERNS.md` — the file the
agents lean on most during real work — because conventions and known gotchas are what keep
the agent inside the project's grain.

```
MODE: explore
SCOPE: docs/context/PATTERNS.md
CONTEXT: Sharpen this project's conventions and known gotchas so the universal agents
  behave correctly here. Use the codebase and docs/context/ as source material.
CONSTRAINT: Do NOT modify .ai-dev-exoskeleton/ files — those are universal.
  Only edit docs/context/ files.
DONE WHEN: PATTERNS.md contains:
  1. Code style + import/naming conventions specific to this project
  2. Test patterns and how the test suite is structured
  3. Stack-specific gotchas (framework quirks, API surprises, common error patterns)
  4. At least one concrete example from this codebase per convention
```

Add gotchas as you hit them: symptom → cause → the rule, with a `file:line` reference.
Every bug that costs more than one round is worth a line here.

## Session 5 (Optional): First Real Task as Validation

Pick a small, low-risk task (bug fix or minor feature) and run through the
full workflow to validate your setup:

```
MODE: debug (or implement)
SCOPE: [small, well-defined area]
CONTEXT: First task on this project — validating my agentic engineering setup.
DONE WHEN: Task completed, tests pass, and the setup felt effective.
```

After this session, do a post-session review (.ai-dev-exoskeleton/guides/checklists/post-session.md):
- Did AGENTS.md provide enough context?
- Did the docs/context/ files give the agent enough architectural understanding?
- Did PATTERNS.md catch the project-specific gotchas you hit?
- What's missing? Update AGENTS.md and docs/context/ accordingly.

---

## Checklist Summary

- [ ] Session 1: Copy .ai-dev-exoskeleton/ into your project repo
- [ ] Session 2: Explore + docs/context/ (incl. its README.md index) + AGENTS.md — structured documentation created
- [ ] Session 2: CLAUDE.md / GEMINI.md pointers to AGENTS.md — added
- [ ] Session 3: Feedback loop — test commands verified and documented in AGENTS.md
- [ ] Session 4: Conventions & gotchas — PATTERNS.md sharpened
- [ ] Session 5: Validation — first real task completed successfully
- [ ] Post-session review — gaps identified and filled

## Time Estimate

| Session | Duration | Output |
|---------|----------|--------|
| Set up exoskeleton | 5 min | .ai-dev-exoskeleton/ folder in your project repo |
| Explore + docs/context/ + AGENTS.md | 20-30 min | 5 context docs + index + project entry file |
| Feedback loop | 10-15 min | Verified test commands documented in AGENTS.md |
| Conventions & gotchas | 15-20 min | Sharpened PATTERNS.md |
| Validation | 15-20 min | First completed task |
| **Total** | **~20-90 min** | **Ready to ship** |

## Tips for Large Legacy Codebases

- Don't try to understand everything in Session 2. Focus on the area you'll work in first.
- If the repo is huge (>1000 files), scope the explore session to one module/service at a time. Create docs/context/ files for each module incrementally rather than trying to document everything at once.
- Ask the team for their "if you could only read 5 files, which ones?" — add those to AGENTS.md Key Files.
- Legacy projects often have undocumented conventions. As you discover them, add to docs/context/PATTERNS.md immediately.
- If there are no tests, your first real task should be adding test infrastructure — agentic engineering without tests is flying blind.
- Start with ARCHITECTURE.md and DEPENDENCIES.md — these provide the most immediate value. Fill in DATA_MODEL.md, API_SURFACE.md, and PATTERNS.md as you work in specific areas.
