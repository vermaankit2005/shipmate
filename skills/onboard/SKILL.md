---
description: Adopt an existing codebase into shipmate — vibe-coded, abandoned, or rescued from another framework. Docs drafted as proposals, stabilize first, then plan forward.
argument-hint: [optional: what you want to do next with this project]
disable-model-invocation: true
---

# /onboard — adopt the project you already have

The product exists; the shipmate state doesn't. Build that state honestly, so every other command works here exactly as if kickoff had started it.

## 1. Learn the codebase (yourself, in the main loop)

Explore proportionately — README, manifests, entry points, module layout, test setup, `git log` for trajectory. Enough to describe what the product does and how it's built; this is orientation, not an audit.

## 2. Draft the docs — as proposals, never as facts

The code tells you what *is*; only the user knows what was *intended* — and the gap between the two is where the bodies are buried. So: draft, **show the user, and let them correct before writing anything**. This confirmation is the one legitimate menu moment of this command. What you can't infer gets `<!-- TODO: confirm -->`, never an invented history.

- `docs/SCOPE.md` — what this product appears to be, for whom; ask the user for non-goals and the riskiest assumption
- `docs/STACK.md` — stack as found, plus the crucial part to establish NOW: **how to run and exercise this product**. If there's a UI and no component library, flag it against the bare-HTML ban and propose the fix as a sprint
- `docs/DECISIONS.md` — seed with the big visible calls, each marked "inferred from code"
- `CLAUDE.md` + `SHIPMATE.md` — same content rules as kickoff (facts + the ~10-line solo-builder ideology; the command cheat sheet)

An existing `docs/` folder with clashing names gets **merged politely** — never overwritten.

## 3. Plan forward — starting with stabilize

"$ARGUMENTS" may say what's next; otherwise ask (once, now, while they're here). Then write `docs/PLAN.md` by kickoff's rules, with one difference: **Sprint 1 is "stabilize"** — get the test suite running and green, fix broken basic flows, cover the scariest core logic. If the codebase is genuinely healthy, say so and propose skipping it — the user decides. Don't plan a rewrite; plan the next milestone of a product that already exists.

Git: init if somehow absent; commit the new docs plainly, no AI co-author trailers.

## Done when

- [ ] User has corrected and approved SCOPE and STACK — unknowns are TODOs, not fiction
- [ ] "Run and exercise it" works on this machine, verified by actually doing it once
- [ ] PLAN.md exists: stabilize sprint (or explicit skip) + the next real sprints + a release sprint
- [ ] Docs committed

Close with: "Adopted. `/shipmate:sprint` picks up from here."
