---
name: follow-up
description: Send a running coding agent a message through Trailboss, now or once its turn ends. Use when asked to tell, remind or instruct another agent that runs in a Herdr or tmux terminal.
requires: trailboss >= 0.4, api 1
---

# Follow up with an agent

First run `trailboss version --json`. If it fails, or `version` is below 0.4 or `api` isn't 1, stop and tell the user to update Trailboss.

1. Find the agent: `trailboss --json live`. Use its `terminal` (`t3`, `herdr:t3`, `tmux:work:2.1`), not its title.
2. Write the message to stand alone: the agent may have compacted its context. Say what to do and why, with names and paths, not "as discussed".
3. Check who would get it: `trailboss --json send --to <terminal> "<message>"`. Every skip comes with a reason (working, waiting on its own dialog, `your draft is in the input`, no terminal).
4. Send it: add `--yes`. Read each row's `action`: `sent`, `held` (the agent will take it after its turn), `no reaction`, or `skipped`.

**Mid-turn agents:** add `--queue` and the message is typed once the turn ends. Queued messages are delivered only while `trailboss watch`, `trailboss events` or the Herdr block runs; if a row says `nothing_looking: true`, tell the user. `trailboss --json queue` shows what waits and what was typed; `trailboss queue rm <id>` takes one back.

Rules:

- Send only what the user asked you to send, to the agents they named. `--to all` only when they say all.
- Never answer another agent's permission prompt or dialog through `send`; Trailboss skips those, so tell the user instead.
- Don't resend because of `no reaction`: check `trailboss --json live` first.
