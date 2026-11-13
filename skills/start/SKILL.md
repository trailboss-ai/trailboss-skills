---
name: start
description: Start one coding agent from a Trailboss agent definition in a new Herdr or tmux terminal, in a folder as it is, with no worktree or branch. Use when asked to open, launch or spin up another agent for a question, an investigation or a conversation, rather than a task to merge.
requires: trailboss >= 0.5, api 1
---

# Start one agent

First run `trailboss version --json`. If it fails, or `version` is below 0.5 or `api` isn't 1, stop and tell the user to update Trailboss.

**Start or task?** `trailboss start` runs the agent in the folder you name, on whatever branch is checked out there: no worktree, no branch, nothing to accept. Use it when the agent reads, answers or investigates, or when the user will work with it directly. When the agent should change code that gets reviewed and merged, use a task instead (the `dispatch` skill).

1. Pick a definition: `trailboss agents` lists them (a kind such as `claude` or `codex`, yours, or the repository's); `trailboss agents show NAME` shows the command it runs.
2. Write its first prompt to stand alone, at least two words: what to do, where, and when it's done. Or leave it out and the agent starts with only the definition's rules, or waits for the user.
3. Show the plan: `trailboss --json start <definition> [--task "<prompt>" | --task-file F] [--in DIR] [--name LABEL]`. Tell the user the `command` and `folder`.
4. Start it with `--yes` only once the user agrees. A host must be running. It opens in a new terminal, nested under this session (or `--parent`).

The label (`--name`, default the definition's name) names its terminal and shows as `label` in `trailboss --json live` and `resume`. Use it to find the agent again; send it messages with the `follow-up` skill.

A repository's definition needs the user's approval first: if `start` refuses one, show the user `trailboss agents trust <name>` and let them approve it; never approve one yourself.
