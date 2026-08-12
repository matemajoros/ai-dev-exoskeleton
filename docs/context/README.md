# Project Context — Index

This folder is the **per-project fill-in** for the AI Dev Exoskeleton. The agents in
`.ai-dev-exoskeleton/` are universal; everything specific to THIS codebase lives here.
Generated during onboarding (see
`.ai-dev-exoskeleton/guides/workflows/new-project-onboarding.md`).

An agent reads this index first, then loads the files relevant to its mode. On a small
repo, reading all of them is cheap — do that. On a large repo, scope down to what the
current task needs.

## Files

| File | Holds | Read it when |
|------|-------|--------------|
| `ARCHITECTURE.md` | Directory map, architecture pattern, module boundaries, entry points, deploy | planning, reviewing, cross-service debugging |
| `PATTERNS.md` | Code style, naming, imports, error handling, test patterns | implementing, reviewing |
| `DATA_MODEL.md` | Entities, relationships, schema, ORM/data-access patterns, migrations | planning, data-layer work |
| `API_SURFACE.md` | Endpoints/CLI, request/response shapes, auth, external integrations | API work, integration debugging |
| `DEPENDENCIES.md` | Tech stack + versions, key deps, config files, env vars, dev/test commands | onboarding, debugging, setup |

Every claim in these files should cite a source (`file:line`) so it can be verified and
kept honest. If a change contradicts something here, the docs may be stale — fix them.
