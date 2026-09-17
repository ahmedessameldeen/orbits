# The six stages

Who drives, what happens, and what has to be true before the next stage starts. Read the
section for the stage you are entering. Do not read ahead.

---

## O — Overview

**Driven by:** person + orchestrator

- Read the primary record, not a summary — the ticket *and its comments*, the defect and its
  occurrences, the PR and its inline comments, the design and its tokens.
- **Get the number.** How many people hit this, how often, since when, on what versions.
  Record the metric, the *exact query*, the value, the date and the release.
- Which number depends on what kind of work this is:

```
Fixing something that exists   → the trailing number, measured before
Building something new        → the leading number, defined before, measured after
Neither applies                → say what you will watch, and what would make you regret it
```

  New work has numbers too; they are leading rather than trailing. Adoption of the new path,
  completion rate of the flow it sits in, time to first success, support contacts about the
  thing it replaces. "No baseline" is an honest answer for a fix. It is rarely the honest
  answer for a feature.
- The third line is not a formality. A change nobody can name a regret condition for is a
  change nobody can evaluate — better to surface that here than at the follow-up.
- Confirm the claim against the code. Reports often describe a symptom whose cause is
  elsewhere.
- Pull the design now, not at review time.
- Other agents read breadth cheaply — call sites, prior art, whether the stated cause fits the
  code. They get the ticket text too, and may push back on it.

**Abort conditions.** Say it and stop if the ticket is already fixed, describes another
system's behaviour, or is not worth the cost.

> **GATE — Overview**
> The problem statement is agreed, and it carries a baseline number — or a reasoned
> "none available".

Record the baseline in the shape given in `metrics.md` before stating this gate.

---

## R — Resolve

**Driven by:** person + orchestrator

- Two or three real approaches — not one plus two strawmen. If there is genuinely one sensible
  way, say so.
- Cost each on files touched, blast radius, data migration, reversibility, and fit with the
  existing code.
- Recommend one, with the reason. A survey with no recommendation pushes the orchestrator's
  job onto the person.
- **Name the target metric** — what should move, by how much, when to check, and what would
  say it did *not* work.
- Choose the method deliberately: test-first, follow-the-neighbour, design-first, model-first,
  or measure-first.

**Method selection.**

| Method | Use when |
|---|---|
| Test-first | The bug is reproducible in a test, and the test is the specification |
| Follow-the-neighbour | A sibling feature already solves this shape of problem well |
| Design-first | The change is user-visible and a design frame exists |
| Model-first | The data shape is the hard part and the UI follows from it |
| Measure-first | Nobody yet knows where the cost actually is |

> **GATE — Resolve**
> One approach chosen and the target metric agreed. The rejected options are recorded too —
> that list ages well.

---

## B — Break down

**Driven by:** orchestrator

- Impact first — who calls this, what breaks. High risk goes to the person *before* anything
  is dispatched.
- Read the neighbouring code: how siblings wire dependencies, name things, and write their
  tests.
- List problems already in the code being touched. Each gets a verdict — fix now, file a
  ticket, or note. **Default is file a ticket**, so the change stays reviewable.
- Simplicity pass: fewer files? any abstraction used once? would the boring version work?
- Chunk it — three files or fewer each, its own gate command, written acceptance criteria,
  **riskiest chunk first**.
- **Permission pre-flight** (see `permissions.md`), so Implement runs without stopping.
- Decide now what the PR will show, and write the design doc.

**Blast radius.** Rate the change LOW / MEDIUM / HIGH / CRITICAL and say why. HIGH or CRITICAL
goes to the person before dispatch, in every mode.

**The cause is elsewhere.** The most common discovery at this stage is that the problem is not
where the ticket said it was. That is a return to **Overview**, not a quiet rewrite of the
problem statement — the baseline was recorded against the stated cause and may no longer be the
right number.

> **GATE — Break down**
> The plan is approved and the permissions are cleared. Backing out here costs one
> conversation; backing out at Test costs a week.

---

## I — Implement

**Driven by:** implementer, chunk by chunk

- One chunk per brief, and the brief is self-contained — assume no memory of the repo. Use the
  brief template in `templates.md`.
- Standing authorisation included, or the reply comes back as a design and the question "shall
  I proceed?". Break down was the planning; the brief is the approval.
- Effort dialled per chunk, not per task: cheap for mechanical work, expensive for concurrency
  and migrations.
- Each chunk's diff reviewed against that chunk's criteria, and its gate run first-hand, before
  the next begins.
- Findings get fixed *or defended*. When a defence is right, the finding is dropped — plainly.

**The chunk loop.**

```
 Write the brief ─► Implementer ─► Read the diff ─► Chunk gate ─► Next chunk
 criteria + rules   own sandbox    + run the gate    criteria      or the
 + source           own context    yourself          met?          stage gate
                         ▲               │
                         │            findings
                         │               ▼
                         └──────────  Argue it
                    same session       fix it, or defend it
                    2 rounds max
```

A hundred lines reviewed in four passes of twenty-five beats a hundred reviewed once — because
when chunk two is wrong, chunks three and four have not been built on top of it yet.

The implementer reading and typing in its own context is where the saving comes from — far
more than choosing a cheaper model. Two rounds caps any single disagreement; after that it goes
to the person with both positions, and nothing lands.

> **GATE — Implement**
> Every chunk green, then the full suite. Two failures on one chunk means the plan was wrong —
> go back to Break down, do not grind.

---

## T — Test

**Driven by:** person, then orchestrator

- **A human exercises the change in a real environment before it ships.** Not a test suite
  standing in for a person — a person, on the real thing, from an exact script.

| What you build | "In your hands" means |
|---|---|
| Mobile / desktop app | The build on a device, from an exact script |
| Web front end | The change in a browser, on the states it affects |
| Backend service | A real request against a running instance, response inspected |
| Library / SDK | A consumer project built against it |
| Data pipeline / infra | A dry run on real-shaped data, output diffed against current |

- Naming the setup matters: some bugs are invisible without a specific device setting, feature
  flag, account state or data shape in place.
- UI work is compared against the design frame and its tokens — the numbers, not the vibe.
  Previews added for the states this change affects.
- **Capture the pictures here**, while the build is on a device and the state is set up. Ship
  needs them and reconstructing them later costs far more. See `evidence.md`.
- Then every gate, run first-hand: code review, formatter, linter, the full suite, coverage.
  A tool that cannot run locally is *said* not to have run.

**The manual test script handed to the person.**

```
BUILD     the exact command
PATH      how to reach the thing that changed
BEFORE    what it used to do
AFTER     what it should do now
SETUP     device settings, flags, accounts, data, network state
WATCH     the one thing most likely to be subtly wrong
```

Right code solving the wrong thing returns to **Resolve**, not to Implement.

> **GATE — Test**
> A human exercised it in a real environment, and every gate is green with numbers from runs
> you performed yourself.

---

## S — Ship

**Driven by:** orchestrator

- **Findings first, PR second.** Say what the diff contains and what was left out, before
  creating anything.
- Stage files by name, never a bare add-all. Commit and push only when the person asks.
- **Attach the proof** — before and after, side by side. For a fix, the "before" is the
  argument.
- PR body in simple English, one screen or less. Design notes in a collapsed section.
- Link back: the PR onto the ticket, and every adjacent finding marked TICKET during Break down
  gets filed now.
- **Name the rollout.** The weeks between merge and evidence are where bad releases live, and
  nothing else in the flow is watching them.

```
ROLLOUT     flag · staged · straight to everyone
KILL        how this gets turned off, and by whom, without a new release
THRESHOLD   the number that says revert now, not "wait for the follow-up"
WATCH       who is looking, for how long
```

  The revert threshold is not the failure condition agreed at Resolve. The failure condition
  asks *did this work*. The threshold asks *is this actively hurting*. A change can clear the
  second and fail the first for weeks.

- **File the follow-up** that re-runs the baseline query once the release has real adoption.
  It carries a **named owner** — a person, not a team — and its trigger is a **condition**
  rather than a date. Without it the orbit never closes.

> **GATE — Ship**
> PR open with proof attached, linked to the ticket, the rollout and revert threshold named,
> and the follow-up filed with an owner and a trigger.

---

## Closing the loop

**A merged pull request is a claim, not evidence.** The evidence arrives weeks later, in the
data. This is the step almost every team skips, and it is the reason the flow is called ORBITS.

Full detail in `metrics.md`.
