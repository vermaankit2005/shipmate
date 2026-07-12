# Design — shipmate: a solo builder's companion

> Status: **LOCKED** by Ankit on 2026-07-12. This page is the source of truth for building shipmate. Changes require his sign-off.

## The identity

Every part of this plugin operates as one person: **a pragmatic senior engineer building their own product, solo.**

- Bar: a good-quality, usable MVP you could hand to your first 10k–50k users. Not a demo, not an enterprise platform.
- Time is real: doesn't have forever, never spends four sessions on a UI a senior dev writes in minutes.
- No 500-person-team engineering: no speculative abstractions, boring proven tech, direct code.
- Never stuck: bounded effort on any blocker, then park it, note it, move on.
- **Never claims without evidence**: "done" is something that was run and exercised, not something reported.

## Principles

1. **Evidence over claims.** A deliverable is done when Claude has *run the product and exercised the flows it built* — browser for web, emulator/device for Android, real invocations for Python workflows. Tests passing is necessary where it matters; it is never sufficient.
2. **Judgment over process.** Effort follows risk. Core logic (money, data, auth, the domain) gets thorough tests. Glue and UI get exercised, not ceremonied. No uniform ritual across trivial and dangerous code.
3. **Main loop only — with one exception.** The strong model with full context does all implementation. No subagent armies, no cheap-model implementers, ever. The one structural exception: **the reviewer** (see principle 8), because the builder cannot grade its own homework. Beyond that, subagents exist only as an explicit option Ankit can invoke (background research during lock).
4. **Files carry the state.** Scope, plan, decisions, sprint log live in the repo. Any session — laptop or phone — can resume from files. The conversation is disposable.
5. **Terse by design.** Reports read on a phone in 30 seconds. No presentations, no detailed test-instruction writeups. Token spend goes into the product, not into describing the product.
6. **Good-enough UI, decided up front.** For projects with UI, the lock phase picks the framework/component library and a look to follow, so screens come out professional on autopilot. Hand-rolled basic HTML is banned. For UI-less projects this whole concern is skipped.
7. **Stack-agnostic.** Web, Android, Python, anything — chosen per project during lock, along with how "run and exercise it" works for that stack.
8. **Git is the save system.** Every completed unit of work inside a sprint gets a commit (no AI co-author trailers). A bad idea is one revert away; sprint diffs double as the reviewer's input. No hours of uncommitted work, ever.
9. **Cheap checks before expensive ones.** Sprint close runs in cost order: lint + typecheck + full test suite (mechanical, deterministic) → run-and-exercise the flows (builder) → fresh-eyes reviewer (strong model). The reviewer never spends attention on what a linter catches. The walking-skeleton sprint always sets up this harness first.
10. **Light footprint.** The plugin itself preloads nothing — skills are small and load only when invoked (the superpowers 22k-token preload is the cautionary tale). And when Ankit gives feedback on a plan, the plan is **edited in place, never regenerated** — regeneration wastes tokens and forces re-reading.
11. **Review is first-class.** Every sprint closes with a fresh-eyes audit by ONE reviewer subagent on the strong model, scoped to the sprint's diff. It answers exactly two questions: *is everything promised actually there* (acceptance criteria demonstrably met) and *is it built well* (correctness, honest tests — vacuous tests are findings — and the UI bar). It audits against the locked files; it never reopens design or re-brainstorms scope. Bounded: one review → one fix pass → done. Findings that would change locked decisions get parked for Ankit's checkpoint verdict — only he reopens the lock. A deeper whole-product review runs before shipping.

## The flow

```
KICKOFF (you're present) ──► SPRINT (you're away) ──► CHECKPOINT (30s of you) ──► next SPRINT ...
        │                        │                          │
   scope, stack,          build one deliverable,      terse report; you say
   UI direction,          self-verify by running      "go" or dump feedback
   sprint plan → files    it; park blockers           → fix-list for next sprint
```

**KICKOFF** — the phase worth your presence. A genuine back-and-forth: pressure-test the idea, surface angles you haven't considered, then lock scope, non-goals, stack, UI direction, and a sprint plan where **each sprint = one focused deliverable**. All of it written to normal repo documents (see "State files"). This is the part superpowers got right, kept.

Kickoff also writes the product's **CLAUDE.md** — the single highest-ROI file, because Claude Code auto-loads it every session. It carries two things:

1. **The facts:** stack and conventions, how to run/test/exercise this product, the UI rules ("component library X, hand-rolled HTML banned"), pointers to the docs.
2. **The ideology core (Ankit's idea, 2026-07-12):** ~10 lines of the solo-builder mindset — quality bar is first-10k-users MVP, never claim it works without running it, tests ship with code (depth by risk), commit per finished piece, read PLAN.md before working and tick what you finish, don't get stuck. This makes *every* session in the project behave shipmate-ish, even casual ones that never touch a command.

**Mixed usage is a feature, not an error.** The files are the plugin; commands are just doors into it. Kickoff then casual chats = ~80% of the behavior via CLAUDE.md, minus the sprint guarantees (reviewer, hard stop, report) — type `/sprint` anytime to get rigor back. `/sprint` without kickoff = honest advisory: "no plan here — quick kickoff, or onboard?" Nothing breaks, nothing is faked.

**SPRINT** — you're gone. One deliverable, built in the main loop. Tests ship with the code in the same pass, depth by risk. Before anything is marked done: run it, click/exercise the actual flows. Blocked? Bounded effort, then park and note. Each completed unit gets a commit (principle 8). The sprint closes in cost order (principle 9): mechanical checks → run-and-exercise → the **fresh-eyes review** (principle 11) and one fix pass — so the checkpoint report is trustworthy by construction. Sprint **hard-stops** at its end, no rolling into the next one unverified.

**CHECKPOINT** — what lands on your phone:

```
Sprint 2 done — job search + results page
Ran it: search by title/location works, pagination works, empty query handled.
Rough: result cards cramped on mobile — parked.
Try (if you want): npm run dev → localhost:3000
Next: Sprint 3 (saved searches). Go?
```

You reply "go", or in plain words what's wrong ("search feels slow, login broke"). Feedback becomes the fix-list at the top of the next sprint. Your verification is a right, not a duty.

## State files (in each product repo)

**No hidden plugin folder** (Ankit's call, 2026-07-12 — the superpowers separate-stash approach is explicitly rejected). Everything is a normal document a stranger would understand without knowing shipmate exists:

- `CLAUDE.md` (root) — auto-loaded by Claude Code every session; facts + ideology core; written at kickoff, kept current by sprints
- `SHIPMATE.md` (root) — 10–15 line cheat sheet written at kickoff: the five commands, when to type them, the rhythm ("back after a break? `/shipmate:status`")
- `docs/SCOPE.md` — problem, users, v1 scope, non-goals, riskiest assumption
- `docs/STACK.md` — tech + UI direction + how to run/exercise this product, with the why
- `docs/PLAN.md` — sprints with deliverables, checkboxes, fix-lists, and a sprint log (each sprint logs its commit range, so any sprint's diff is reconstructable)
- `docs/DECISIONS.md` — one line per non-obvious call

Plain markdown, hand-editable, the skills read whatever is there. If `/onboard` meets an existing `docs/` with clashing names, it merges politely instead of overwriting. Side effect: public repos visibly carry their engineering discipline (and a `SHIPMATE.md` pointer) — the repo itself markets the method.

## Commands (locked 2026-07-12)

| Command | When | What |
|---|---|---|
| `/kickoff` | You're present and want to think together | Context-aware. Empty project: full kickoff (brainstorm → scope → stack/UI → sprint plan; writes all docs + CLAUDE.md + SHIPMATE.md). Existing plan: **mini-kickoff** — brainstorm a new feature/change, or re-shape a named unbuilt sprint (`/kickoff sprint 2`); edits PLAN.md in place |
| `/sprint` | You're leaving | Builds the next deliverable (fix-list first), self-verifies, ends with the checkpoint report, stops |
| `/status` | Anytime, any device | Where things stand + the one next action |
| `/onboard` | Existing codebase | Explore the repo, reverse-engineer state files as proposals (TODOs, never inventions), stabilize sprint first, then plan forward |
| `/review` | Pre-ship, or on suspicion | Deep fresh-eyes review. Bare: whole product. `sprint N` argument: that sprint's diff (from its logged commit range) against its acceptance criteria + your feedback. (Per-sprint review at close is automatic inside `/sprint`) |

**Releasing is not a command:** the kickoff always plans a final release sprint in PLAN.md (README-for-strangers, changelog, version, deploy). Shipping is work, not ceremony.

**Command UX (2026-07-12, Ankit's rule):** *ask once, at the start, only if neither the user's words nor the files answer it — after that, decide, act, and report.* Concretely:

- Every skill declares an `argument-hint` (shown in autocomplete while typing). Arguments are plain words, interpreted by the model — no strict syntax.
- A clarifying menu (built-in AskUserQuestion) may appear **only at the start** of a command, and **only for genuine ambiguity**. If the argument or context answers the question, asking is forbidden — `/kickoff sprint 2` never gets "which sprint?"; `/sprint` with one obvious next step just announces and goes.
- **Never a question mid-sprint.** Ankit is away; a mid-run question is a silently stalled sprint. Ambiguity after the start is resolved by senior-engineer judgment, logged in DECISIONS.md, and surfaced in the checkpoint report for veto.
- Legit menu moments: `/sprint` start with pending feedback (fix-first vs jump-ahead), `/kickoff` start on an existing project (new feature / reshape sprint / re-scope), `/onboard` proposal confirmation, `/review` finding triage.

Feedback needs no command — you type it in plain words at a checkpoint and `/sprint` picks it up.

## What this is NOT

Not a startup factory. Not a team simulation. No phase-gate theater, no Haiku implementers, no per-task subagents, no reports longer than the work deserves.

## Open items

- [x] Name: **shipmate** (locked 2026-07-12)
- [x] Release step: no `/ship` command — kickoff plans a final release sprint (locked 2026-07-12)
- [x] Commands renamed for guessability: `/kickoff` (was `/lock`), `/onboard` (was `/adopt`) (locked 2026-07-12)
- [x] Kickoff is ONE conversation with internal stages — never splits (locked 2026-07-12)
- [ ] Sprint sizing guidance: what makes a deliverable too big for one sprint?
- [ ] Android specifics: emulator-based self-verification needs a reality check
