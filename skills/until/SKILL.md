---
name: until
description: Keep a coding agent working until a check such as the test suite passes, with Trailboss's until loop, and steer running loops. Use when asked to have an agent keep going until tests, a build or a linter pass.
requires: trailboss >= 0.4, api 1
---

# Keep an agent going until a check passes

First run `trailboss version --json`. If it fails, or `version` is below 0.4 or `api` isn't 1, stop and tell the user to update Trailboss.

1. Pick the session (`AGENT:ID`, a session id, or its terminal from `trailboss --json live`) and a check the user agrees to. It runs as the user, without a shell, in the session's folder after every turn: `-- cargo test`, or `-- sh -c 'npm run build && npm test'`.
2. Set limits that fit the job, flags before `--`:

   ```sh
   trailboss until --max-rounds 5 --max-cost 2 --max-hours 1 --detach t3 -- cargo test
   ```

   Defaults: 10 rounds, $5, 2 hours, and a 10-minute `--check-timeout`. `--detach` keeps it running after this terminal closes; without it, the command holds this terminal until the loop stops.
3. Watch: `trailboss --json until ls` (each loop's `state`, `round`, `last_passed`, `cost_usd`, and `log` for a detached one).
4. Steer: `trailboss until pause|resume|stop <loop id|session|terminal>`. Use `all` only when the user says so.

When it stops, report why (`stopped` and `reason` in the last `--json` line or the log): passed, a limit, no progress, or the session ended. Don't start a second loop on the same session; Trailboss refuses it.
