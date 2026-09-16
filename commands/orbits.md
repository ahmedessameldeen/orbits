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
5. When the person opens the gate, read the next stage's section and repeat.

## The stages and their gates

| Stage | Gate |
|---|---|
| Overview | Problem agreed, and it carries a baseline number — or a reasoned "none available" |
| Resolve | One approach chosen, one target metric agreed |
| Break down | Plan approved, permissions cleared |
| Implement | Every chunk meets its criteria, then the full suite |
| Test | Works in the person's hands, all gates green from runs you performed yourself |
| Ship | PR with proof, linked to the ticket, follow-up filed |

## Standing rules for this run

- Agents write the code. **Never commit, never push** unless the person asks.
- Never paste file contents into the conversation — cite a path and a line number.
- A claim of green is not evidence. Re-run the gates first-hand, with real numbers.
- Abort is a valid outcome at Overview and Break down. Say it and stop.
- Two rounds on any disagreement, then put both positions to the person.

If the person would rather batch the gates, use `/orbits-autopilot` instead.
