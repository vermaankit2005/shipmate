<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo-dark.svg">
    <img src="assets/logo.svg" width="150" alt="shipmate — a line-art sailboat">
  </picture>
</p>

<h1 align="center">shipmate</h1>

<p align="center">
  <b>Your AI shipmate for solo product development.</b><br>
  A companion, not a framework — silent until you call it.<br>
  And nothing is <i>done</i> until it's been <b>run, clicked, and reviewed</b>.
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue" alt="MIT license"></a>
  <img src="https://img.shields.io/badge/Claude_Code-plugin-d97757" alt="Claude Code plugin">
  <img src="https://img.shields.io/badge/subagents-one._just_one.-0a1d33" alt="one subagent">
</p>

---

<h3 align="center">The AI said all tests passed.<br>Then you opened the app.</h3>

## What hurts

Every "AI engineering team" framework fails solo builders the same way:

- You hand over an idea → it spawns an **army of subagents**
- Cheap models implement tickets they don't understand
- Every phase reports success — *tests written, review passed, approved*
- **Nobody ever runs your product.** Not once. Not one flow.
- Weeks of tokens and late nights later: the basic flows don't work
- You paid for an engineering team. You got one unsupervised intern.

## The fix is one rule

> **A claim is worthless. Evidence is everything.<br>
> If it wasn't run, it doesn't work.**

Everything in shipmate follows from it:

- **One strong model, full context, builds everything** — no agent army, no cheap-model interns
- Before anything is marked done, shipmate **starts your product and uses it** — clicks the flows, runs the commands
- **One fresh-eyes reviewer audits every sprint** — the only subagent in the entire system
- **Everything is versioned automatically** — a git commit after every finished piece; any bad idea is one revert away
- Tests ship with the code — deep where the risk lives, light where it doesn't
- You read an **8-line report** and reply "go" — that's your whole job

## A companion, not a framework

- **Silent until called.** No hooks, no preloaded skills, zero ambient context — your normal chats stay 100% yours. Type a command or shipmate doesn't exist
- **Doesn't eat your money.** Costs nothing when idle; when working, tokens go into the product — never into ceremony about the product
- **Joins at any phase.** Fresh idea → `/shipmate:kickoff`. Half-built repo — vibe-coded, abandoned, or rescued from another framework → `/shipmate:onboard` adopts it: reads the code, drafts the missing docs as proposals, stabilizes what's shaky, plans forward
- **Leaves no lock-in.** Stop anytime — what remains is a well-documented repo, not a dependency

## Install

```
/plugin marketplace add vermaankit2005/shipmate
/plugin install shipmate@shipmate-marketplace
```

Start something new:

```
/shipmate:kickoff a tool that <your idea>
```

Or hand over the half-built project you already have: `/shipmate:onboard`.

## The rhythm

```
KICKOFF ────────────► SPRINT ────────────► CHECKPOINT ────► next SPRINT …
you're present         you're away          30 seconds of you
```

**Kickoff** — the only phase that needs you:

- A real back-and-forth: pressure-tests your idea, surfaces angles you missed
- Locks scope, stack, and UI direction — a proper component library, never bare HTML
- Plans sprints where **each sprint = one focused deliverable**

**Sprint** — you walk away:

- Builds one deliverable, committing each finished piece — your history is your save file
- Verifies by **running the product**, not by claiming
- Fresh-eyes review + fix pass, then a **hard stop** — never rolls on unverified

**Checkpoint** — 30 seconds, wherever you are:

```
Sprint 2 done — add expense + monthly summary
Acceptance: 5/5 pass — add/edit/delete, totals, empty month all verified live.
Smoke: sprint-1 flows still good.
Reviewed: 2 findings fixed. 1 parked: category colors look dull.
Try (if you want): npm run dev → localhost:3000
Next: Sprint 3 (budgets + alerts). Go?
```

- Reply **"go"** — next sprint starts
- Or say what's wrong in plain words — it becomes the next sprint's fix-list
- Checking the app yourself is your right, never your duty

## Commands

| Command | When | What happens |
|---|---|---|
| `/shipmate:kickoff` | Starting something, or rethinking a sprint | Brainstorm together, lock it into the plan. `kickoff sprint 2` rethinks one sprint |
| `/shipmate:sprint` | You're heading out | Builds the next deliverable, verifies by running it, reports, stops |
| `/shipmate:status` | Coming back after a break | Where things stand + the one next action |
| `/shipmate:onboard` | You have an existing codebase | Adopts it — docs as proposals, stabilize first, plan forward |
| `/shipmate:review` | Pre-ship, or on suspicion | Deep fresh-eyes audit — whole product, or `review sprint 3` |

Questions only when your words and the files don't answer them — once, at the start, **never mid-sprint**.

## What lands in your repo

No hidden plugin folders — just documents a well-run project should have anyway:

```
CLAUDE.md           auto-loaded brief: stack, run commands, solo-builder rules
SHIPMATE.md         15-line cheat sheet: the commands and the rhythm
docs/SCOPE.md       problem, users, v1 scope, non-goals, riskiest assumption
docs/STACK.md       tech + UI direction + how to run and exercise the product
docs/PLAN.md        sprints, checkboxes, fix-lists, sprint log
docs/DECISIONS.md   one line per non-obvious call, with the why
```

**The files are the plugin; commands are just doors.** Work in plain chats anytime — `CLAUDE.md` keeps every session on the rules, and `/sprint` brings the guarantees back whenever you want them.

## What shipmate is NOT

- Not a startup factory — no PM/architect/QA personas
- Not a team simulation — you are the team; shipmate is the companion
- Not an agent army — one model building, one reviewing
- Not a ceremony engine — no reports longer than the work they describe

## Straight answers

- **Any stack?** Web, Android, Python, CLIs. Kickoff decides what "run it" means per project; no-UI projects skip the UI rules
- **Token cost?** Zero until invoked. The deliberate spends — verification runs and one reviewer per sprint — exist to prevent the expensive thing: confident work on a broken product
- **Do I babysit it?** No. Lock, leave, read 8 lines, say "go"

---

<p align="center">
  Built by a solo developer, for solo developers — from the scar tissue of doing it the other way.<br>
  <b>MIT licensed.</b> If shipmate shipped something for you, a star helps other builders find it.
</p>
