---
name: orbits-stage
description: Enter the ORBITS flow at a named stage — overview, resolve, breakdown, implement, test or ship — for work already in progress.
argument-hint: "overview | resolve | breakdown | implement | test | ship"
---

# /orbits-stage

Enter the flow at: $ARGUMENTS

If no stage was named, say which stage the work appears to be at, and why, then ask the
person to confirm before proceeding.

## How to run it

1. Load the `orbits` skill and read **only** that stage's section in `references/stages.md`.
2. Confirm in one line what the previous gate established. If the previous gate was never
   opened, say so — entering mid-flow without it is how a run ends up with no baseline and
   no target.
3. Do the stage. Produce its output in the fixed shape from `references/templates.md`.
4. State the gate and stop.

## Entering without the earlier gates

Two things are load-bearing and are worth reconstructing before continuing:

- **The baseline number** (Overview). Without it the orbit cannot close, because there is
  nothing to re-run later.
- **The target metric and its failure condition** (Resolve). Without it "did it work?" has no
  answer.

If either is missing, get it now rather than carrying on without it. It costs a few messages
here and a whole release cycle later.
