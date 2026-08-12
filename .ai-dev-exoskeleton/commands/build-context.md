# /build-context — Feature Q&A Mode

Lightweight Q&A routine to build mutual understanding of a feature before planning. No code, no planning — only context gathering and a final `CONTEXT.md` write.

## Quick Rules
- NEVER implement code
- NEVER write `PLAN.md` — that is the planner’s job, invoked manually afterwards
- ONLY write a single markdown file: `docs/tasks/[yyyymmdd-short-description]/CONTEXT.md`
- Goal: mutual alignment on requirements, constraints, scope, and exclusions

## Process

### Phase A — User builds context
Tell the user:
```
"Build your context. Tell me everything I need to know about this feature —
business requirements, technical constraints, UX decisions, what's in scope,
what's out of scope. I'll respond OKE until you're done."
```
Respond **OKE** to every user message until the user signals they are done (e.g., "that's it", "ready", "done with context", or asks you to proceed).

Why the bare acknowledgement: while the user is dumping context, any commentary,
question, or suggestion from the agent interrupts their train of thought and drags the
conversation into premature problem-solving. `OKE` (any short ack works — "ok", "noted")
keeps the channel open and the user in flow. The agent's turn to ask comes in Phase B.

### Phase B — Agent asks clarifying questions
Once the user is done, ask YOUR questions:
- What is unclear or ambiguous?
- Are there edge cases not covered?
- Are there implicit assumptions that should be explicit?
- What is explicitly OUT of scope?

The user answers. Keep asking follow-ups until you have no more questions.

### Phase C — Mutual confirmation
When both sides have no more questions, confirm:
```
"I believe we're aligned. Shall I create the task folder and write CONTEXT.md?"
```
Do NOT proceed until the user confirms.

### Step 2 — Create task folder + CONTEXT.md
Once the user confirms, create the task folder at `docs/tasks/[yyyymmdd-short-description]/` and write `CONTEXT.md`:

```markdown
# [Feature Name] — Context

## Jira / Ticket
[reference or "—"]

## Business Requirements
- [requirement 1]
- [requirement 2]

## UX / Design Decisions
- [decision 1]
- [decision 2]

## Technical Decisions
- [decision 1]
- [decision 2]

## Open Questions That Were Resolved
- Q: [question] → A: [answer]

## Exclusions
- [what is NOT in scope]
```

This file preserves the Q&A knowledge so that a new session (e.g., the planner) can rebuild context from it without re-doing the Q&A.

### Done
After writing `CONTEXT.md`, stop and tell the user:
```
"CONTEXT.md is ready at docs/tasks/[folder]/CONTEXT.md.
Next step: manually invoke the planner agent with a fresh session so it reads CONTEXT.md and produces PLAN.md."
```

Do NOT invoke the planner yourself. Do NOT continue to implementation. This routine ends here.

## Anti-Patterns to Avoid
- Do NOT skip Phase A (user context dump) — even if the user seems eager to start
- Do NOT start asking questions before the user signals they are done
- Do NOT write `CONTEXT.md` before mutual confirmation
- Do NOT write `PLAN.md` or any code file
- Do NOT invoke other agents (planner, implementer, etc.) — the user does that manually afterwards
