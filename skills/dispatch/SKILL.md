---
name: dispatch
description: Hand work to new coding agents with Trailboss tasks, each in its own git worktree and branch, then review and merge what they did. Use when asked to start, check on or accept tasks run by other agents.
requires: trailboss >= 0.4, api 1
---

# Dispatch tasks

First run `trailboss version --json`. If it fails, or `version` is below 0.4 or `api` isn't 1, stop and tell the user to update Trailboss.

## Start

1. Write a self-contained brief: the task, when it's done (a check that passes), the files involved, what must stay intact, and any rules. The agent sees nothing else. It must be at least two words: a one-word brief is refused.
2. Show the plan: `trailboss task add "<brief>" [--agent NAME] [--folder DIR]`. Several tasks: repeat `--brief "<text>"` or `--brief-file F`, or pass `--brief-file` a folder of `.md`/`.txt` briefs. Read the warnings: two briefs naming the same file will collide.
3. Start with `--yes` only once the user has agreed to the plan. Each task gets a worktree on `work/<n>-<slug>` and a new Herdr or tmux terminal, nested under this session. A host must be running.

`--agent` takes a kind (`claude`, `codex`, `gemini`, `copilot`, `opencode`, `pi`) or a definition's name. `trailboss agents` lists the definitions; `trailboss agents show NAME` shows the command one runs. A repository's definitions need the user's approval before first use (`trailboss agents trust <name> --yes`): if `task add` refuses an unapproved one, show the user `trailboss agents trust <name>` and let them approve it; never approve one yourself.

Don't do a dispatched task's work yourself in parallel.

## Check on them

`trailboss --json task ls`: each task's `state` (to do, working, needs you, ready, done), commits and files. Report in a short table, starting with what only the user can decide (`needs you`, `ready`).

## Accept

1. `trailboss --json task show <n>`: read `summary`, `changed`, `checks` and `can_accept` / `accept_blocked`. Summarize them for the user.
2. Merge only when the user says so: `trailboss task accept <n> --yes` (fast-forward only; refused when the checkout has uncommitted changes).
3. To drop a task: `trailboss task rm <n> --yes`. It keeps unmerged commits and uncommitted changes; never add `--force` unless the user asks.
