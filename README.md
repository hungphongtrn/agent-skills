# Agent Skills

A collection of skills for AI-assisted development.

## Engineering Skills

These skills are located in the `skills/engineering/` directory:

| Skill | Description |
|-------|-------------|
| diagnose | Disciplined diagnosis loop for hard bugs and performance regressions |
| finishing-a-development-branch | Guide branch, PR, source issue update, and cleanup after implementation |
| grill-with-docs | Stress-test plans against project's domain language and documented decisions |
| improve-codebase-architecture | Find deepening opportunities for better testability and AI-navigability |
| requesting-code-review | Request code reviews to catch issues before they cascade |
| setup-project-skills | Required bootstrap for GitHub Issues, labels, workflow instructions, and domain docs |
| subagent-driven-development | Execute implementation plans with independent tasks using fresh subagents and two-stage review |
| tdd | Test-driven development with red-green-refactor loop |
| to-issues | Break PRDs or issues into smaller GitHub issues using vertical slices |
| to-prd | Turn conversation context into an intent-level PRD and publish to GitHub Issues |
| triage | Triage GitHub issues through category and state roles |
| using-git-worktrees | Set up isolated workspaces before implementation work |
| writing-plans | Write implementation plans using progressive disclosure — detailed tasks for current phase only, future phases stubbed |
| zoom-out | Get broader context and higher-level perspective on code |

## Usage

To use a skill in a conversation, reference it by name or load it explicitly.

For engineering skills, run `setup-project-skills` in each repo first. It configures GitHub Issues as project memory, installs or verifies `WORKFLOW.md`, and writes the repo's agent instructions.

After setup, agents should follow this instruction from `AGENTS.md` or `CLAUDE.md`:

```markdown
When using skills under `skills/engineering/`, first consult `WORKFLOW.md` to choose the appropriate workflow. Treat this file as the workflow router and operating model; treat individual `SKILL.md` files as the detailed procedures.
```

## Setting Up In A New Project

Engineering skills require GitHub Issues as durable project memory. Set up each greenfield or brownfield repo through `setup-project-skills`:

1. **Install engineering skills** using the skills CLI:
   ```bash
   # List available skills first
   npx skills add hungphongtrn/agent-skills --list

   # Install all engineering skills
   npx skills add hungphongtrn/agent-skills

   # Or install specific skills only
   npx skills add hungphongtrn/agent-skills --skill diagnose --skill tdd --skill writing-plans
   ```

2. **Run setup in the target repo** by asking your coding agent:
   ```text
   Run setup-project-skills for this repo.
   ```

   The setup skill verifies GitHub access, creates or maps required labels, installs or verifies `WORKFLOW.md`, updates `AGENTS.md` or `CLAUDE.md`, and writes `docs/agents/*` configuration files.

3. **Use the workflow through GitHub Issues**:
   ```text
   Use triage to show me what to work on next.
   Execute issue #6.
   ```

## Adding New Skills

Skills can be installed to one of the following directories:
- `~/.claude/skills/`
- `~/.config/opencode/skills/`
- `~/.agents/skills/`

Or kept within this repository under `skills/engineering/`.
