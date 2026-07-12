---
description: Orient in the current product — where things stand, what happened last, and the one next action. Read-only, fast, no ceremony.
disable-model-invocation: true
---

# /status — where am I?

The anti-lost command. The user may be returning after days or weeks; give them their bearings in under a minute of reading. Read-only — change nothing.

1. Read `docs/PLAN.md` (current status line, checkboxes, sprint log tail), skim `docs/SCOPE.md` and the recent `docs/DECISIONS.md` entries. Check `git log --oneline -5` and `git status` — uncommitted work is part of "where am I".
2. Report in a few short paragraphs, not a wall of sections:
   - **Where you are:** which sprint, its deliverable, done vs remaining overall.
   - **Last session:** what the sprint log says actually happened, including anything parked, half-done, or failing. Honest, not rosy.
   - **The one next action:** be decisive — a single recommendation, not a menu. Usually "run `/shipmate:sprint` — next is Sprint N: <deliverable>". Pending feedback unaddressed → say that's what `/sprint` will pick up first. Everything built → `/shipmate:review` before the release sprint.
3. **Flag drift** if you see it: uncommitted changes with no log entry, ticked boxes with no commit range, a stale status line. Offer to reconcile — but only do it if asked; status is read-only by default.

No `docs/PLAN.md`? Then this project isn't under shipmate yet — recommend `/shipmate:kickoff` (new idea) or `/shipmate:onboard` (existing code), one line each, done.
