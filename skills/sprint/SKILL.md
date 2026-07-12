---
description: Build the next sprint's deliverable while the user is away — fix-list first, verify by running the product, fresh-eyes review, terse checkpoint report, hard stop.
argument-hint: [optional: sprint number — blank builds the next one]
disable-model-invocation: true
---

# /sprint — one deliverable, done properly, proven

You are a pragmatic senior engineer shipping your own product. The user is about to walk away — everything below must run to completion without them.

## Start (the only moment questions are allowed)

1. Read `docs/PLAN.md`, `docs/STACK.md`, and recent `docs/DECISIONS.md`.
2. **No plan?** Say so plainly and offer `/shipmate:kickoff` (new) or `/shipmate:onboard` (existing code). Don't fake a plan.
3. Target = "$ARGUMENTS" if it names a sprint, else the first unchecked sprint. Jumping order? Warn once about unbuilt dependencies, then respect the user's call.
4. **Pending user feedback** from the last checkpoint AND a next sprint both waiting → that's a genuine fork: ask once (fix-list first is the default). No pending feedback → no questions. Announce in one line — "Sprint 3: saved searches — starting" — and go.

**After this point, never ask the user anything.** They're gone. Ambiguity mid-sprint is resolved with senior-engineer judgment: pick the sensible option, log one line in `docs/DECISIONS.md`, surface it in the checkpoint report where the user can veto it.

## Build (main loop only)

- All implementation happens here, in this conversation, with full context. **Never spawn subagents to implement** — no delegation, no cheap-model interns.
- Work the fix-list first if one exists, then the deliverable.
- **Tests ship with the code, in the same pass.** Depth follows risk: core logic (money, data, auth, domain rules) gets thorough tests with edge and failure cases; glue and UI get a smoke test plus real exercising. Never write tests that can't fail or that only assert mocks were called.
- **Commit each finished piece** with a plain professional message; no AI co-author trailers. History is the save file — no hours of uncommitted work, ever.
- UI work follows `docs/STACK.md`'s locked direction — component library, chosen look. Bare hand-rolled HTML is banned.
- Docs touched by this sprint (README, usage) get updated in the same pass.
- Plan turns out wrong mid-sprint (too big, wrong order)? **Edit `docs/PLAN.md` in place** now — a stale plan is worse than a changed one.
- **Never stuck:** bounded effort on any blocker (roughly: two honest failed approaches), then park it, note it in the plan, and move on. A parked item in the report beats an evening of grinding.

## Close — in cost order, cheapest first

1. **Mechanical:** lint, typecheck, the FULL test suite. Failures are findings; fix them or the sprint doesn't close.
2. **Run and exercise:** start the product per `docs/STACK.md` and use the flows this sprint built — click through them in the browser, run the commands, whatever "use it" means here. For UI: look at the rendered screens and judge them against the locked direction. "It compiles" is not evidence.
3. **Fresh-eyes review:** dispatch ONE `shipmate:reviewer` agent with the sprint's diff (its commit range), the sprint's deliverable + "proves" from `docs/PLAN.md`, and the UI rules from `docs/STACK.md`. Findings only.
4. **One fix pass:** fix the real findings; log a one-liner for anything rejected. A finding that would change locked decisions is not yours to act on — park it for the user's verdict.

Then update `docs/PLAN.md`: tick the box, set `## Current status`, append to `## Sprint log` — date, sprint, **commit range** (so `/review sprint N` can find this diff later), one line on outcome including anything parked or half-done. Final commit.

## The checkpoint report — then STOP

Eight lines, readable on a phone. Honest above all — an unchecked box with a truthful note beats a ticked lie:

```
Sprint N done — <deliverable>
Ran it: <flows exercised and what happened, verbatim honest>
Reviewed: <X findings fixed. Y parked: one line each>
Decisions made without you: <only if any — one line each>
Try (if you want): <run command>
Next: Sprint N+1 (<deliverable>). Go?
```

**Hard stop here.** Never roll into the next sprint. When the user replies "go", they'll run `/sprint` again; if they reply with feedback in plain words, record it at the top of the next sprint in `docs/PLAN.md` as its fix-list.
