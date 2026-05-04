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

## Adding New Skills

Skills can be installed to one of the following directories:
- `~/.claude/skills/`
- `~/.config/opencode/skills/`
- `~/.agents/skills/`

Or kept within this repository under `engineering/`.
