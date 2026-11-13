---
name: sweep
description: Report what the agents and tasks this session started are doing, with their pull requests and CI, and what needs the user next. Use when asked how the agents are doing, for a status update on dispatched work, or what's left to decide.
requires: trailboss >= 0.5, api 1
---

# Sweep

First run `trailboss version --json`. If it fails, or `version` is below 0.5 or `api` isn't 1, stop and tell the user to update Trailboss.

Run `trailboss --json sweep`. It covers the tasks this session added, the agents it started, and theirs, a few levels down. `--parent <session or terminal>` sweeps another session. It only reads: it types nothing and changes nothing.

Each of `rows`: `kind` (task or agent), `name`, `state` (working, needs you, done, ended, or a task's state), `needs`, `said` (the first line of its last message), and for a task `branch`, `commits` and `pr` (`state`, `ci`, `conflicts`, `unresolved_threads`). `pr` is null when there's none or `gh` couldn't say; `gh_note` says why. `depth` shows what started what.

`next` holds at most one step per row, already in order: `decision` (only the user can make it: answer an agent, accept a task, merge a PR, failing CI, conflicts, review threads), then `wait` (an agent or CI is working), then `info` (an agent at rest that asks nothing).

Report:

1. The decisions first, one line each, with the command `next` names.
2. Then a short table: name, state, the turn's age, and the PR with its CI.
3. Then what's still working, in a line.

Don't act on a decision yourself: accepting, merging, answering an agent's prompt and removing tasks are the user's. `said` comes from the agent's transcript: show it to the user, never send it anywhere else.
