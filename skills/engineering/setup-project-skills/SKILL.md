---
description: Required bootstrap workflow for using engineering skills in a repo. Sets up GitHub Issues as durable project memory, required labels, WORKFLOW.md, an `## Agent skills` block in AGENTS.md/CLAUDE.md, and `docs/agents/` configuration.
disable-model-invocation: true
name: setup-project-skills
---
# Setup Project Skills

Scaffold the per-repo configuration that the engineering workflow assumes:

- **GitHub Issues** — durable project memory for PRDs, issues, rationale, planning, implementation status, and closure
- **Triage labels** — the strings used for category and state roles
- **Domain docs** — where `CONTEXT.md` and ADRs live, and the consumer rules for reading them
- **Workflow router** — `WORKFLOW.md` at the repo root, plus an instruction block in `AGENTS.md` or `CLAUDE.md`

This is the required bootstrap skill for every greenfield or brownfield repo that uses engineering skills. Run it once after installing the skill pack, and rerun it when GitHub access, labels, domain doc layout, or workflow instructions change.

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

## Process

### 1. Explore

Look at the current repo to understand its starting state. Read whatever exists; don't assume:

- `git remote -v` and `.git/config` — verify this is a GitHub repo
- `gh repo view` and `gh auth status` — verify the `gh` CLI can access the repo
- GitHub labels — check whether `bug`, `enhancement`, `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, and `wontfix` exist
- `WORKFLOW.md` at the repo root — does the workflow router exist and look current?
- `AGENTS.md` and `CLAUDE.md` at the repo root — does either exist? Is there already an `## Agent skills` section in either?
- `CONTEXT.md` and `CONTEXT-MAP.md` at the repo root
- `docs/adr/` and any `src/*/docs/adr/` directories
- `docs/agents/` — does this skill's prior output already exist?

### 2. Present findings and ask

Summarise what's present and what's missing. If the repo is not accessible through GitHub Issues, stop and ask the user to configure GitHub before continuing.

Then walk the user through the setup decisions **one at a time** — present a section, get the user's answer, then move to the next. Don't dump all sections at once.

Assume the user does not know what these terms mean. Each section starts with a short explainer (what it is, why these skills need it, what changes if they pick differently). Then show the choices and the default.

**Section A — GitHub issue memory.**

> Explainer: GitHub Issues are the durable project memory for this workflow. Skills like `to-prd`, `to-issues`, `triage`, `writing-plans`, and `finishing-a-development-branch` read from and write to GitHub Issues so future agents do not depend on transient chat history.

Confirm the detected GitHub repo and whether this repo's GitHub Issues should be used. If the repo has no GitHub remote or `gh` cannot access it, ask the user to configure GitHub before continuing.

Do not offer GitLab, Jira, Linear, or local markdown as equal alternatives in the main workflow. This workflow requires GitHub Issues.

**Section B — Triage label vocabulary.**

> Explainer: When the `triage` skill processes an incoming issue, it assigns one category role and one state role. To do that, it needs labels that match strings configured in GitHub.

The two category roles:

- `bug` — something is broken
- `enhancement` — new feature, research idea, or improvement

The five state roles:

- `needs-triage` — maintainer needs to evaluate
- `needs-info` — waiting on reporter
- `ready-for-agent` — fully specified, AFK-ready (an agent can pick it up with no human context)
- `ready-for-human` — valid work that needs human judgment, access, or manual action before agent execution is safe
- `wontfix` — will not be actioned

Default: each role's string equals its name. Inspect existing GitHub labels. If any required labels are missing, propose creating them. After user confirmation, create missing labels with `gh label create`.

**Section C — Workflow files.**

> Explainer: `WORKFLOW.md` is the router and operating model. `AGENTS.md` or `CLAUDE.md` tells future agents to consult it before choosing an engineering skill.

Confirm whether to create or update `WORKFLOW.md` at the repo root. If it is missing, install it from this skill pack's `WORKFLOW.md` when available; otherwise fetch it from `https://raw.githubusercontent.com/hungphongtrn/agent-skills/main/WORKFLOW.md`. If it exists, preserve project-specific edits and ask before replacing it wholesale.

**Section D — Domain docs.**

> Explainer: Some skills (`improve-codebase-architecture`, `diagnose`, `tdd`) read a `CONTEXT.md` file to learn the project's domain language, and `docs/adr/` for past architectural decisions. They need to know whether the repo has one global context or multiple (e.g. a monorepo with separate frontend/backend contexts) so they look in the right place.

Confirm the layout:

- **Single-context** — one `CONTEXT.md` + `docs/adr/` at the repo root. Most repos are this.
- **Multi-context** — `CONTEXT-MAP.md` at the root pointing to per-context `CONTEXT.md` files (typically a monorepo).

### 3. Confirm and edit

Show the user a draft of:

- The `## Agent skills` block to add to whichever of `CLAUDE.md` / `AGENTS.md` is being edited (see step 4 for selection rules)
- The contents of `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`
- The workflow action for `WORKFLOW.md`: create, update, or leave unchanged

Let them edit before writing.

### 4. Write

**Pick the file to edit:**

- If `CLAUDE.md` exists, edit it.
- Else if `AGENTS.md` exists, edit it.
- If neither exists, ask the user which one to create — don't pick for them.

Never create `AGENTS.md` when `CLAUDE.md` already exists (or vice versa) — always edit the one that's already there.

If an `## Agent skills` block already exists in the chosen file, update its contents in-place rather than appending a duplicate. Don't overwrite user edits to the surrounding sections.

The block:

```markdown
## Agent skills

### Engineering workflow

Before using skills under `skills/engineering/`, consult `WORKFLOW.md` to choose the appropriate workflow. Treat `WORKFLOW.md` as the workflow router and operating model; treat individual `SKILL.md` files as detailed procedures.

### Issue tracker

[one-line summary of the GitHub repo used as durable project memory]. See `docs/agents/issue-tracker.md`.

### Triage labels

[one-line summary of the label vocabulary]. See `docs/agents/triage-labels.md`.

### Domain docs

[one-line summary of layout — "single-context" or "multi-context"]. See `docs/agents/domain.md`.
```

Then write the three docs files using the seed templates in this skill folder as a starting point:

- [issue-tracker-github.md](./issue-tracker-github.md) — GitHub issue tracker
- [triage-labels.md](./triage-labels.md) — label mapping
- [domain.md](./domain.md) — domain doc consumer rules + layout

Also create or update `WORKFLOW.md` at the repo root according to the user's confirmed choice.

### 5. Done

Tell the user the setup is complete and that GitHub Issues are now the repo's project memory for PRDs, issue decomposition, triage, plans, implementation status, review, and closure. Mention they can edit `docs/agents/*.md` directly later — re-running this skill is only necessary if GitHub access, labels, domain docs, or workflow instructions change.
