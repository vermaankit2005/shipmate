---
name: onboard
description: Adopt an existing codebase into shipmate — vibe-coded, abandoned, or rescued from another framework. Docs drafted as proposals, stabilize first, then plan forward.
argument-hint: [optional: what you want to do next with this project]
disable-model-invocation: true
---

# /onboard — adopt the project you already have

The product exists; the shipmate state doesn't. Build that state honestly, so every other command works here exactly as if kickoff had started it.

## 1. Learn the codebase — by reading AND by running it

Explore proportionately — README, manifests, entry points, module layout, test setup, `git log` for trajectory. Then **run it**: start the product and exercise its main flows; run the test suite. Reading tells you what was written; running tells you what the user actually has — and what's broken, flaky, or won't even start is the most important thing you'll learn today. Note every failure; the stabilize sprint will be built from this list, not from guesses.

## 2. Give your honest read — then draft the docs as proposals

Before drafting anything, tell the user what you found, as a peer looking at their codebase for the first time: what's solid, what's scary, what breaks first, what surprised you. Include your candidate for the riskiest assumption and the non-goals you'd guess — propose, let them correct. This is a conversation, not a form.

Then the docs. The code tells you what *is*; only the user knows what was *intended* — and the gap between the two is where the bodies are buried. So: draft, **show the user, and let them correct before writing anything**. This confirmation is the one legitimate menu moment of this command. What you can't infer gets `<!-- TODO: confirm -->`, never an invented history.

- `docs/SCOPE.md` — what this product appears to be, for whom; non-goals and riskiest assumption as corrected by the user above
- `docs/STACK.md` — stack as found, plus the crucial part to establish NOW: **how to run and exercise this product**. If there's a UI and no component library, flag it against the bare-HTML ban and propose the fix as a sprint
- `docs/DECISIONS.md` — seed with the big visible calls, each marked "inferred from code"
- `CLAUDE.md` + `SHIPMATE.md` — same content rules as kickoff (facts + the ~10-line solo-builder ideology; the command cheat sheet)

An existing `docs/` folder with clashing names gets **merged politely** — never overwritten.

## 3. Plan forward — starting with stabilize

"$ARGUMENTS" may say what's next; otherwise ask — once, now, while they're here; use AskUserQuestion if the answer is a genuine pick-from-options, plain text if it isn't (the tool's built-in "Other" covers custom answers — treat those as first-class). In the same breath, ask kickoff's **quality gates** question (AskUserQuestion: tests + fresh-eyes review / tests only / review only / manual) — an inherited codebase without tests may honestly not want them — and record the answer under `## Quality gates` in `docs/STACK.md`. Then write `docs/PLAN.md` by kickoff's rules — same goal/tasks/acceptance format, same risk ordering — with one difference: **Sprint 1 is "stabilize"**, and its tasks come straight from what step 1 exposed: the failing tests (if the gates include tests), the broken flows, the setup that didn't work on this machine, the scariest uncovered core logic. If running it exposed nothing — product starts, flows work, tests green — say so and propose skipping stabilize; the user decides. Don't plan a rewrite; plan the next milestone of a product that already exists.

Git: init if somehow absent; commit the new docs plainly, no AI co-author trailers.

## Done when

- [ ] You ran the product and the tests, and gave the user your honest read before drafting any doc
- [ ] User has corrected and approved SCOPE and STACK — unknowns are TODOs, not fiction
- [ ] "Run and exercise it" works on this machine, verified by actually doing it once
- [ ] Quality gates chosen by the user via AskUserQuestion and recorded in `docs/STACK.md`
- [ ] PLAN.md exists: stabilize sprint (or explicit skip) + the next real sprints + a release sprint
- [ ] Docs committed

Close with: "Adopted. `/shipmate:sprint` picks up from here."
