# Superpowers (Agent Teams Fork)

A fork of [obra/superpowers](https://github.com/obra/superpowers) that adds **agent team execution** as a third plan execution option, alongside the existing subagent-driven and inline execution approaches.

## What This Fork Changes

This fork makes three targeted changes to the upstream superpowers plugin:

1. **New skill: `agent-team-execution`** — Execute implementation plans using Claude Code's [agent teams](https://code.claude.com/docs/en/agent-teams) feature. Implementer teammates work independent tasks in parallel, a dedicated reviewer teammate handles spec + quality review, and the team lead coordinates batches.

2. **Modified: `writing-plans` handoff** — The plan completion prompt now offers three execution options instead of two: Subagent-Driven, Agent Team, and Inline Execution.

3. **Modified: model selection** — All execution approaches always use the most powerful available model.

Everything else is unmodified from upstream.

## When to Use Agent Teams vs Subagents

| Aspect | Subagent-Driven | Agent Team |
|--------|----------------|------------|
| Parallelism | Sequential (one task at a time) | Parallel batches |
| Communication | Implementer reports to lead only | Teammates message each other |
| Best for | Plans with tightly coupled tasks | Plans with independent tasks |
| Token cost | Medium | Higher (multiple teammates) |

Use **subagent-driven** (the default) for most plans. Use **agent teams** when the plan has batches of tasks that don't share files and would benefit from parallel execution.

## Prerequisites

- Claude Code v2.1.32+
- Agent teams enabled:
  ```json
  // settings.json
  {
    "env": {
      "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
    }
  }
  ```

## Installation

If you have the official superpowers plugin installed, uninstall it first:

```
/plugin uninstall superpowers@claude-plugins-official
```

Then install this fork:

```
/plugin marketplace add harrymunro/superpowers-agent-teams
/plugin install superpowers@harrymunro-superpowers-agent-teams
```

## Updating

This fork syncs with upstream weekly via GitHub Actions. To update:

```
/plugin update superpowers
```

## Upstream

This fork tracks [obra/superpowers](https://github.com/obra/superpowers). For full documentation, contributing guidelines, community support, and sponsorship information, see the upstream repository.

## License

MIT License — see [LICENSE](LICENSE) file. Original work by [Jesse Vincent](https://github.com/obra).
