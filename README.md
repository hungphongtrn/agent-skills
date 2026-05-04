# Agent Skills

A collection of skills for AI-assisted development.

## Engineering Skills

These skills are located in the `engineering/` directory:

| Skill | Description |
|-------|-------------|
| subagent-driven-development | Execute implementation plans with independent tasks using fresh subagents and two-stage review |
| writing-plans | Write implementation plans using progressive disclosure — detailed tasks for current phase only, future phases stubbed |
| triage | Triage issues through a state machine driven by triage roles |
| to-prd | Turn conversation context into a PRD and publish to issue tracker |
| to-issues | Break plans into independently-grabbable issues using vertical slices |
| tdd | Test-driven development with red-green-refactor loop |
| setup-project-skills | Scaffold per-repo configuration for issue tracker, triage labels, and domain docs |
| improve-codebase-architecture | Find deepening opportunities for better testability and AI-navigability |
| grill-with-docs | Stress-test plans against project's domain language and documented decisions |
| diagnose | Disciplined diagnosis loop for hard bugs and performance regressions |
| zoom-out | Get broader context and higher-level perspective on code |

## Usage

To use a skill in a conversation, reference it by name or load it explicitly.

## Adding New Skills

Skills can be installed to one of the following directories:
- `~/.claude/skills/`
- `~/.config/opencode/skills/`
- `~/.agents/skills/`

Or kept within this repository under `engineering/`.
