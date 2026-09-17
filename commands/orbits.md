---
name: orbits
description: Run a piece of work through the ORBITS flow from the beginning — Overview, Resolve, Break down, Implement, Test, Ship — stopping at every gate.
argument-hint: "<ticket URL, defect id, bug description, or feature request>"
---

# /orbits

Run this work through the ORBITS flow: $ARGUMENTS

If nothing was given, ask what the work is before doing anything else.

## How to run it

1. Load the `orbits` skill. Read `references/stages.md` for **Overview only**.
2. Start at **Overview**. Do not skip ahead because the fix looks obvious — the number is
   the point, not the fix.
3. Produce the stage's output in the fixed shape from `references/templates.md`.
4. State the gate and **stop**. Do not begin the next stage, and do not keep working while
   the gate is discussed.
5. When the gate opens, write what the stage produced into the run file, then read the next
   stage's section and repeat.

Open a run file at Overview and update it at every gate — the shape is in
`references/templates.md`. It is what lets this run survive a lost session, change hands, and
be closed weeks later by `/orbits-check`.

## The stages and their gates

| Stage | Gate |
|---|---|
| Overview | Problem agreed, and it carries a number — trailing for a fix, leading for new work |
| Resolve | One approach chosen, one target metric agreed |
| Break down | Plan approved, permissions cleared |
| Implement | Every chunk meets its criteria, then the full suite |
| Test | A human exercised it in a real environment, all gates green from runs you did yourself |
| Ship | PR with proof, rollout and revert threshold named, follow-up filed with an owner |

## Standing rules for this run

- Agents write the code. **Nothing leaves the machine without the person asking** — no push,
  no PR, no ticket writes, no deploys.
- **A new requirement is a new orbit.** Do not fold it into this run.
- Never paste file contents into the conversation — cite a path and a line number.
- A claim of green is not evidence. Re-run the gates first-hand, with real numbers.
- Abort is a valid outcome at Overview and Break down. Say it and stop.
- Two rounds on any disagreement, then put both positions to the person.

If the person would rather batch the gates, use `/orbits-autopilot` instead.
