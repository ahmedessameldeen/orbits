---
name: orbits
description: Run software work through the ORBITS flow — Overview, Resolve, Break down, Implement, Test, Ship — six stages from a measured problem to a verified fix, each ending at a gate a person opens. Use when picking up a bug, ticket, defect, feature or refactor; when planning an approach or breaking work into chunks; when briefing or delegating to another coding agent; when deciding whether a change is ready to ship; or when checking weeks later whether a shipped fix actually moved the number. Also triggers on "run this through ORBITS", "what stage are we at", "open the gate", "autopilot", "close the orbit".
---

# The ORBITS Flow

Six stages from a **measured problem** to a **verified fix**. Each one ends at a gate that a
person opens. Work does not move forward because it feels finished — it moves forward because
the gate opened.

**O**verview · **R**esolve · **B**reak down · **I**mplement · **T**est · **S**hip

It is called ORBITS because the work comes back around: the follow-up filed at Ship re-enters
at Overview, carrying the number it was opened to check.

Three things hold the whole flow up:

- **A fix is finished when the number moves, not when it merges.**
- **A person opens every gate** — or reviews them in one batch, on autopilot.
- **Agents write the code, never commit.**

## How to use this skill

1. Work out which stage you are in. If work has just arrived, you are at **Overview** — you
   are not allowed to skip to Break down because the fix looks obvious.
2. Read that stage's section in `references/stages.md` **on entry**, not up front.
3. Do the stage. State its gate. **Stop and wait** for the person to open it.
4. Only then start the next stage.

Never run two stages in one turn. Never state a gate and keep working while it is discussed.

## The pipeline

```
 O ───────► R ───────► B ───────► I ───────► T ───────► S
Overview  Resolve   Break down  Implement   Test      Ship
  │          │          │          │          │          │
 gate       gate       gate       gate       gate       gate
  │          │          ▲          │          │          │
  │          ▲          └──────────┘          │          │
  │          │      chunk fails twice →       │          │
  │          │        the plan was wrong      │          │
  │          └─────────────────────────────────┘         │
  │            right code, wrong thing → choose again     │
  └───────────────────────────────────────────────────────┘
     the orbit closes · weeks later · did the number actually move?
```

Every return path starts on the expensive side and lands on the cheap side. That is the
argument for spending real time in Overview and Resolve: those two stages cost messages, and
the stages they protect cost days. The path from Ship back to Overview is different — it is
not a failure, it is the flow closing its own loop.

## The gates

| Stage | Gate — what must be true before the next stage starts |
|---|---|
| **Overview** | The problem statement is agreed, and it carries a baseline number — or a reasoned "none available". |
| **Resolve** | One approach chosen and the target metric agreed. The rejected options are recorded too. |
| **Break down** | The plan is approved and the permissions are cleared. |
| **Implement** | Every chunk green against its own criteria, then the full suite. |
| **Test** | It works in the person's hands, and every gate is green with numbers from runs you performed yourself. |
| **Ship** | PR open with proof attached, linked to the ticket, and the follow-up filed with a date or a trigger. |

## Roles, not product names

Map these onto whatever agents actually exist. One agent can hold several. The only role that
must never collapse into another is the person — the gates exist to be opened by a human.

| Role | Does | Usually |
|---|---|---|
| Person | Opens every gate. Decides. Runs the app. | The human |
| Orchestrator | Owns judgment. Plans, briefs, verifies, argues, lands. | The agent being talked to |
| Implementer | Writes code from a brief, in its own context. | A delegated coding agent, or the orchestrator itself |
| Reviewer | Argues against the diff and the plan. | A second agent, if one exists |
| Analyst | Pulls the numbers — errors, complaints, funnels, adoption. | The orchestrator with analytics tools |

## Rules that hold everywhere

**Gates are hard.** State the gate and wait for it. No starting the next bit while it is
discussed. A gate you skipped is rework you have not paid for yet. On autopilot the gate still
has to be opened and logged — it is answered sooner, not waived.

**Context parity.** Every agent gets the same material the orchestrator has — ticket text,
defect detail, design spec, decisions already made — *pasted into the brief, not linked*. An
implementer without the ticket invents a requirement. One that has it can argue with it, and
that argument is worth having. Where an agent cannot reach a source, the orchestrator carries
the content across.

**Ask, never guess.** An agent missing something it needs asks for it. It is never fenced out
of the reasoning because of what it cannot see for itself.

**Debate needs two agents.** With a second capable agent, findings get argued between agents —
stated as claims with evidence, answered with a fix or a defence. With only one, the
orchestrator puts them to the person. A single agent arguing with itself produces the
appearance of rigour and none of the substance.

**Two rounds, then escalate.** Any single disagreement gets two rounds. Still contested: both
positions stated fairly, a recommendation made, and the person decides. Nothing lands while
contested.

**Talk early, terse late.** Overview and Resolve are cheap and are where the expensive mistakes
get caught — take as many rounds as the problem needs. Implement, Test and Ship are where
brevity pays. Budget the conversation the opposite way round from the instinct.

**Abort is a valid outcome.** At Overview and Break down the honest answer may be that the
ticket is wrong, already fixed, or not worth the cost. Say it and stop. Do not build something
to avoid an awkward conversation.

**A claim is not evidence.** An agent reporting green is making a claim. The gates get re-run
first-hand, with real numbers, every time. Anything not verified is said plainly rather than
left to silence.

**Write for a tired reader.** PRs, tickets and design notes in short, plain sentences. No
idioms. Assume the reader's English is weak and their day is long. A PR description longer
than one screen has failed.

**Comments only where code cannot speak.** A non-obvious *why*, or a workaround with a ticket
link. Never restate the code. Never comment code you did not change.

## Keeping it cheap

Token discipline, stated mechanically rather than hoped for — and spent where it matters, on
the early conversation.

1. **Never paste file contents into the conversation.** Cite a path and a line number.
2. **Implementers read and type in their own context.** None of it lands in the orchestrator's.
   That is the real saving; model tier is a smaller dial on top.
3. **Stage playbooks are read on entry**, not loaded up front.
4. **The implementer's session is reused** for follow-ups rather than re-briefed from scratch.
5. **Review the diff, not the file.**
6. **Fixed output shapes per stage.** No prose padding, no restating what just happened.
7. **No narration.** Tool calls are not announced before they are made.

## References

Read these on entry to the stage that needs them — not up front.

| File | Read it when |
|---|---|
| `references/stages.md` | Entering any stage. The full playbook for all six. |
| `references/metrics.md` | At Overview (baseline), Resolve (target), Ship (follow-up), and when closing the orbit. |
| `references/autopilot.md` | The person asks for autopilot, or asks to batch the gates. |
| `references/permissions.md` | At Break down, during the permission pre-flight. |
| `references/evidence.md` | At Test (capture) and Ship (attach). Any change a user can see. |
| `references/templates.md` | Writing an implementer brief, a decision-log entry, a PR body, or a follow-up ticket. |
