# trailboss-skills

Skills that teach coding agents to drive [Trailboss](https://github.com/trailboss-ai/trailboss): how to use its commands and `--json` output, and what an agent may and may not do with them.

| Skill | What it teaches |
|---|---|
| [`dispatch`](skills/dispatch/SKILL.md) | Hand work to new agents as tasks, each in its own worktree and branch; check on them, review and accept (`task`, `agents`) |
| [`follow-up`](skills/follow-up/SKILL.md) | Send a running agent a self-contained message, now or when its turn ends (`send`, `queue`) |
| [`until`](skills/until/SKILL.md) | Keep an agent going until a check passes, and steer the loop (`until`) |
| [`checkpoints`](skills/checkpoints/SKILL.md) | Save, compare and restore an agent's folder (`checkpoint`) |
| [`start`](skills/start/SKILL.md) | Start one agent from a definition in a folder as it is, outside a task (`start`) |
| [`sweep`](skills/sweep/SKILL.md) | What the agents and tasks this session started are doing, their PRs and CI, and what needs you next (`sweep`) |

Each one arrives with the Trailboss release that ships the commands it describes; these need Trailboss 0.4.

## Install

In Claude Code:

```text
/plugin marketplace add trailboss-ai/trailboss-skills
/plugin install trailboss@trailboss
```

Trailboss itself never writes into an agent's folder; your agent's plugin mechanism installs these.

## Versions

Each skill names the lowest Trailboss version and `--json` API it needs in its front matter, and checks `trailboss version --json` before it does anything:

```yaml
---
name: example
description: When to use this skill.
requires: trailboss >= 0.5, api 3
---
```

`main` only holds skills for commands in a released Trailboss. CI checks every command and flag a skill names against the latest release.

## Layout

```text
.claude-plugin/
  marketplace.json   the marketplace: one plugin, "trailboss"
  plugin.json        the plugin
skills/
  <name>/SKILL.md    one skill, plus any templates it uses
```

## License

[MIT](LICENSE). See [CONTRIBUTING.md](CONTRIBUTING.md) for the contributor terms.
