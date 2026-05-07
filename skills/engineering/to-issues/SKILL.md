---
description: Break a PRD or issue into smaller GitHub issues using tracer-bullet vertical slices. Use recursively until leaf issues are small enough for one agent to plan and execute safely.
name: to-issues
---
# To Issues

Break a PRD or issue into independently-grabbable GitHub issues using vertical slices (tracer bullets).

GitHub Issues and the triage label vocabulary should have been provided to you — run `/setup-project-skills` if not.

Before decomposing a PRD or issue, use `grill-with-docs` to stress-test scope, terminology, dependencies, acceptance criteria, and HITL/AFK boundaries unless the split is purely mechanical and already explicit.

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes an issue reference (issue number or URL) as an argument, fetch it from GitHub and read its full body, comments, labels, and parent/child references.

### 2. Explore the codebase (optional)

If you have not already explored the codebase, do so to understand the current state of the code. Issue titles and descriptions should use the project's domain glossary vocabulary, and respect ADRs in the area you're touching.

### 3. Draft vertical slices

Break the source into **tracer bullet** issues. Each issue is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer.

Slices may be 'HITL' or 'AFK'. HITL slices require human interaction, such as an architectural decision or a design review. AFK slices can be implemented and merged without human interaction. Prefer AFK over HITL where possible.

<vertical-slice-rules>
- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests)
- A completed slice is demoable or verifiable on its own
- Prefer many thin slices over few thick ones
</vertical-slice-rules>

Use this skill recursively when an issue is still too large or ambiguous for one agent to execute safely.

Stop decomposing when each leaf issue is:

- independently understandable from the issue body and comments
- small enough for one branch/PR
- has clear acceptance criteria
- has no unresolved intent, domain, architecture, or scope decisions
- can be planned with `writing-plans` without reopening the parent discussion

### 4. Publish or draft the breakdown

By default, publish the breakdown directly to GitHub. If the user explicitly asks to draft first, present the proposed breakdown as a numbered list. For each slice, show:

- **Title**: short descriptive name
- **Type**: HITL / AFK
- **Blocked by**: which other slices (if any) must complete first
- **User stories covered**: which user stories this addresses (if the source material has them)

If drafting first, ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the dependency relationships correct?
- Should any slices be merged or split further?
- Are the correct slices marked as HITL and AFK?

Iterate until the user approves the breakdown, then publish.

### 5. Publish the issues to GitHub

For each slice, publish a new GitHub issue. Use the issue body template below. Apply the `needs-triage` triage label so each issue enters the normal triage flow.

Publish issues in dependency order (blockers first) so you can reference real issue identifiers in the "Blocked by" field.

<issue-template>
## Parent

A reference to the parent GitHub issue (if the source was an existing issue, otherwise omit this section).

## What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Blocked by

- A reference to the blocking ticket (if any)

Or "None - can start immediately" if no blockers.

</issue-template>

Do NOT close parent issues. If child issues are created from an existing GitHub issue, comment on the parent with the child issue list.
