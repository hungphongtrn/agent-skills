# Agent Skills

A collection of skills for AI-assisted development.

## Engineering Skills

These skills are located in the `engineering/` directory:

| Skill | Description |
|-------|-------------|
| diagnose | Disciplined diagnosis loop for hard bugs and performance regressions |
| finishing-a-development-branch | Guide branch completion with options for merge, PR creation/update, or cleanup |
| grill-with-docs | Stress-test plans against project's domain language and documented decisions |
| improve-codebase-architecture | Find deepening opportunities for better testability and AI-navigability |
| requesting-code-review | Request code reviews to catch issues before they cascade |
| setup-project-skills | Scaffold per-repo configuration for issue tracker, triage labels, and domain docs |
| subagent-driven-development | Execute implementation plans with independent tasks using fresh subagents and two-stage review |
| tdd | Test-driven development with red-green-refactor loop |
| to-issues | Break plans into independently-grabbable issues using vertical slices |
| to-prd | Turn conversation context into a PRD and publish to issue tracker |
| triage | Triage issues through a state machine driven by triage roles |
| writing-plans | Write implementation plans using progressive disclosure — detailed tasks for current phase only, future phases stubbed |
| zoom-out | Get broader context and higher-level perspective on code |

## Usage

To use a skill in a conversation, reference it by name or load it explicitly.

For engineering skills, add this to `AGENTS.md` so agents choose the right workflow first:

```markdown
When using skills under `skills/engineering/`, first consult `WORKFLOW.md` to choose the appropriate workflow. Treat this file as the skill router and the individual `SKILL.md` files as the detailed procedures.
```

## Setting Up In A New Project

When working on a new project, set up the skills and workflow so agents can operate effectively:

1. **Install engineering skills** using the skills CLI:
   ```bash
   # Using GitHub CLI
   gh skills install engineering

   # Or using npx
   npx skills add engineering
   ```

2. **Copy `WORKFLOW.md`** into the project root from the installed skills.

3. **Append the workflow reference** to `AGENTS.md` (create if it doesn't exist):
   ```markdown
   ## Engineering Skills Workflow

   When using skills under `skills/engineering/`, first consult `WORKFLOW.md` to choose the appropriate workflow. Treat this file as the skill router and the individual `SKILL.md` files as the detailed procedures.
   ```

## Adding New Skills

Skills can be installed to one of the following directories:
- `~/.claude/skills/`
- `~/.config/opencode/skills/`
- `~/.agents/skills/`

Or kept within this repository under `engineering/`.
