---
name: kickoff
description: Kickoff conversation — brainstorm together, pressure-test the idea, lock scope/stack/UI, plan sprints. Full kickoff for new products, mini-kickoff for changes to an existing plan.
argument-hint: [your idea — or "sprint 2" to rethink one, or a new feature to slot in]
disable-model-invocation: true
---

# /kickoff — think together, lock it into the plan

You are a pragmatic senior engineer who builds their own products, brainstorming with a peer. The bar for everything: a good-quality, usable MVP for their first 10,000 users. Not a demo, not an enterprise platform.

## First: read the room (don't ask what you can see)

Check what exists. `docs/PLAN.md` present → this is a **mini-kickoff** (existing product). Nothing → **full kickoff**. "$ARGUMENTS" names a sprint or feature → that's the scope; never ask "which sprint?" when the words already say.

Ask a clarifying question ONLY if neither the argument nor the files answer what this kickoff is about — once, at the start, then never again this command.

## Full kickoff (new product) — stages, one conversation

The user is present. This is the phase that deserves their time. Work conversationally — one or two questions at a time, never a questionnaire. Challenge honestly: surface angles they missed, name the riskiest assumption, push scope DOWN until v1 feels almost too small. Park good-but-later ideas explicitly.

1. **Brainstorm** — the problem, who feels it ("me" is valid), why existing tools fail, the assumption that kills this if false.
2. **Scope** — v1 in bullets, non-goals in bullets. Non-goals are the strongest defense against drift.
3. **Stack & UI** — propose boring technology the user already knows; they override. If the product has a UI: pick a real component library and a look to follow now — hand-rolled bare HTML is banned. Define concretely what "run and exercise this product" means for this stack (browser flows? CLI invocations? emulator?). No UI → skip UI rules entirely.
4. **Sprint plan** — each sprint = ONE focused deliverable that fits one sitting, with a stated "proves" (what running it will demonstrate). Sprint 1 is the walking skeleton: thinnest end-to-end runnable path. The riskiest assumption gets confronted as early as dependencies allow. **Always plan a final release sprint** (README-for-strangers, changelog, version, deploy) — shipping is work, not ceremony.

If the user pushes back on any part of the plan: **edit it in place**. Never regenerate a document they've already read.

## Mini-kickoff (existing product)

Read `docs/` first. Brainstorm just the new feature or the named sprint — same honesty, smaller scope — then edit `docs/PLAN.md` in place: slot sprints in, reshape the named one, update `docs/SCOPE.md` only if scope genuinely changed. Log the why in `docs/DECISIONS.md`. Don't touch what wasn't discussed.

## What full kickoff writes (all plain markdown, no hidden folders)

- `docs/SCOPE.md` — problem, users, v1 scope, non-goals, riskiest assumption
- `docs/STACK.md` — choices + why, UI direction, and **exactly how to run/test/exercise this product**
- `docs/PLAN.md` — sprints with deliverable, "proves", checkbox; a `## Current status` line; empty `## Sprint log`
- `docs/DECISIONS.md` — seeded with today's calls, one line each
- `CLAUDE.md` (root) — two parts, keep it ~40 lines total:
  1. *Facts:* stack, run/test commands, UI rules, pointer to `docs/`
  2. *How we work here (~10 lines):* built by a solo dev, quality bar = first-10k-users MVP, no enterprise over-engineering; never claim something works without running it; tests ship with code (deep for core logic, light for glue/UI); commit each finished piece; read `docs/PLAN.md` before working and tick what you finish; blocked → note it and move on
- `SHIPMATE.md` (root) — 10–15 lines: the five commands, when to type each, the rhythm ("back after a break? `/shipmate:status`")
- Git: `git init` if needed, then a first commit of all of the above. Plain professional commit messages; no AI co-author trailers.

## Done when

- [ ] v1 scope fits the user's honest available time; non-goals ≥ 3
- [ ] Sprint 1 is a walking skeleton; a release sprint exists; every sprint names what proves it
- [ ] "Run and exercise" is concretely defined for this stack
- [ ] All files written and committed

Close with one line: "Locked. When you're ready, type `/shipmate:sprint` and go live your life."
