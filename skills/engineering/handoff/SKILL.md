---
name: handoff
description: Create a focused handoff for continuing paused multi-phase work. Use when the user wants to hand off work to a future session, pause a multi-phase implementation, or prepare context for an AFK agent.
---

# handoff

Use this skill when work is mid-flight and a fresh agent must resume quickly.

## What this produces
A concise handoff message returned directly to the user. No file is created, no commit is made. The handoff is a text artifact the user can copy, paste, or forward.

## First step: extract the goal
The user may provide a goal inline when invoking this skill, for example:
- `/handoff Complete the data pipeline`
- `/handoff Fix the failing test in src/auth.ts`

Read the user's message and extract any goal text that follows the invocation. Any text after `/handoff` **is** the goal. Do not ask for the goal if it was already provided.

If no goal was provided inline (bare `/handoff` or implicit invocation), ask the user for one explicit continuation goal. Examples of valid goals:
- "Detail Phase 2 and implement it"
- "Complete the data pipeline"
- "Fix the failing test"

**Do not proceed** without a concrete goal sentence, either extracted from the message or confirmed by the user.

## Context gathering (focused, not exhaustive)
Read only the minimum required context:
1. Plan `README.md` and `strategy.md` for big-picture intent and phase map.
2. `decisions.md` for accumulated learnings, corrections, and rationale.
3. Source GitHub issue body for requirements/acceptance criteria.
4. The current/relevant phase document.
5. Only source files that were modified already or are directly relevant to the next step.

Do not re-read the whole repository. Do not restate broad architecture already covered in the plan unless it is required for the next action.

## Handoff content contract (include only these sections)
The handoff must contain:
1. Current state (what is done, what is pending)
2. Goal (the next objective)
3. Key learnings from completed work (surprises, corrections, gotchas)
4. Exact file paths of what was built/changed
5. Links/paths to the plan and source issue
6. Available modules/APIs that can be reused next
7. Exact next steps for the pickup agent

## Quality bar
- Keep it one screen: under ~100 lines.
- Treat handoff as a BRIDGE:
  - not a replacement for the plan,
  - not a codebase rehash,
  - not a conversation transcript.
- Focus on the delta between:
  - what the plan originally said, and
  - what implementation taught us.

## Output
- Return the handoff content directly to the user as a markdown message.
- Do **not** write it to a file.
- Do **not** commit it to git.
- Keep wording actionable and specific.
