---
description: Turn the current conversation context into an intent-level PRD and publish it to GitHub Issues. Use when user wants to capture current context as durable project memory.
name: to-prd
---
This skill takes the current conversation context and codebase understanding and produces an intent-level PRD. Do NOT interview the user — synthesize what you already know. If critical ambiguity remains, record it as an open question instead of resolving it silently.

GitHub Issues and the triage label vocabulary should have been provided to you — run `/setup-project-skills` if not.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already. Use the project's domain glossary vocabulary throughout the PRD, and respect any ADRs in the area you're touching.

2. Write the PRD using the template below, then publish it to GitHub Issues. Apply the `needs-triage` triage label so it enters the normal triage flow.

Publish directly unless the user explicitly asks to draft first. GitHub is the working memory; uncertainty belongs in the issue body under open questions or assumptions.

3. Report the created issue URL/number and the recommended next step, usually `grill-with-docs` followed by `to-issues` for decomposition.

<prd-template>

## Problem Statement

Why this work matters and what problem, opportunity, or research question motivated it.

## Desired Outcome

The high-level outcome that should be true when this work succeeds.

## User Stories

A numbered list of user stories, research goals, or stakeholder outcomes. For product work, use:

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

For research or infrastructure work, adapt the format to capture the actor, desired capability, and reason.

## Constraints

Constraints that are already known, such as compatibility, data, runtime, deployment, research, safety, or operational constraints.

## Non-Goals

What this PRD intentionally does not cover.

## Open Questions

Important ambiguity that should be resolved during `grill-with-docs`, triage, issue decomposition, or planning.

## Assumptions

Assumptions made while synthesizing the current conversation. These are not final decisions unless later confirmed.

## Further Notes

Any further notes about the work.

</prd-template>
