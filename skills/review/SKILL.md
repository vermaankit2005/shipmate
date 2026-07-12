---
name: review
description: Deep fresh-eyes audit on demand — whole product before shipping, or one sprint on suspicion. Never reopens design; findings get one fix pass.
argument-hint: [blank for whole product, or "sprint 3" for one sprint]
disable-model-invocation: true
---

# /review — the deep audit

Per-sprint review already happens automatically inside `/sprint`. This command is for the two other moments: the whole-product pass before shipping, and re-examining one sprint because the user's gut says something's off.

## Scope (from the words, not from a question)

- "$ARGUMENTS" names a sprint → that sprint's diff, reconstructed from the **commit range logged in `docs/PLAN.md`'s sprint log**, judged against that sprint's deliverable and "proves", plus any user feedback about it.
- Blank → the whole product against `docs/SCOPE.md`: every v1 promise, checked against the running product.

## 1. Mechanical first (cheap before expensive)

Lint, typecheck, full test suite — report results verbatim. Docs drift: does the README/setup still match reality? Plan drift: ticked boxes vs actual code and commits.

## 2. Run it

Whole-product mode: start the product per `docs/STACK.md` and walk the core flows a real user would — this is where "the login button did nothing" gets caught. Sprint mode: exercise the flows that sprint claims.

## 3. Fresh eyes

Dispatch ONE `shipmate:reviewer` agent with the scope (diff or product), the acceptance criteria from `docs/PLAN.md` / `docs/SCOPE.md`, and the UI rules from `docs/STACK.md`. Findings only, ranked, verified.

## 4. Triage with the user — they're present for this command

Merge everything into one ranked list and present it (a triage menu is appropriate here):

- **Fix now** — correctness bugs, promises not actually kept, dishonest tests. Fix in the main loop, one pass.
- **Queue** — real but not blocking → append to `docs/PLAN.md` as sprint items so they don't evaporate.
- **Reject** — noise; one line why.

Review is **bounded**: one review → one fix pass → done. Findings that would change locked decisions (scope, stack, architecture) are never acted on here — they're presented for the user's verdict, because only the user reopens the lock. No re-brainstorming, no loops.

## Close

Append a review entry to the sprint log (date, scope, outcome). Commit fixes plainly, no AI co-author trailers. End with one line: what was fixed, what was queued, and — if this was the pre-ship pass — whether the product is honestly ready for the release sprint.
