---
name: checkpoints
description: Save, compare and restore a coding agent's working folder with Trailboss checkpoints (git commits kept apart from your branches). Use before a risky change, or when asked to see or undo what an agent did in a stretch of work.
requires: trailboss >= 0.4, api 1
---

# Checkpoints

First run `trailboss version --json`. If it fails, or `version` is below 0.4 or `api` isn't 1, stop and tell the user to update Trailboss.

A checkpoint is the session's folder (tracked files, plus untracked ones git doesn't ignore) saved as a commit under `refs/trailboss/checkpoints/`. Saving never changes the index, `HEAD`, branches or stash, and nothing is pushed. Sessions are `AGENT:ID` (from `trailboss --json live` or `sessions`).

- **Save:** `trailboss checkpoint save AGENT:ID --label "<what this is>"`. Nothing is saved if nothing changed.
- **See:** `trailboss --json checkpoint list AGENT:ID`, then `trailboss checkpoint diff AGENT:ID N` for what N changed.
- **Restore:** first `trailboss --json checkpoint restore AGENT:ID N` and show the user which files it would write and remove. Only when they agree, add `--yes`: it saves a safety checkpoint and keeps every file it replaces in Trailboss's undo folder first. It's refused while the session is working or needs the user; never add `--force` unless they ask.
- **Automatic:** folders listed in the config's `checkpoints.auto` get a checkpoint at the end of every turn, while `trailboss watch` or `events` runs. Changing the config is the user's call.
- **Tidy up:** `trailboss checkpoint prune [FOLDER]` shows the checkpoints of removed worktrees; `--yes` drops them.
