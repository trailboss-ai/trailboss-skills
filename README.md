# trailboss-skills

Skills that teach coding agents to drive [Trailboss](https://github.com/trailboss-ai/trailboss): how to use its commands and `--json` output, and what an agent may and may not do with them.

There are no skills here yet. Each one arrives with the Trailboss release that ships the commands it describes.

## Install

In Claude Code:

```text
/plugin marketplace add trailboss-ai/trailboss-skills
/plugin install trailboss@trailboss
```

Trailboss itself never writes into an agent's folder; your agent's plugin mechanism installs these. `trailboss skill` prints the short built-in guide.

## Versions

Each skill names the lowest Trailboss version and `--json` API it needs in its front matter, and checks `trailboss --version` before it does anything:

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
