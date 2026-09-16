---
name: orbits-autopilot
description: Run the ORBITS flow with the first four gates self-opened and logged, handing back to the person at Test. For routine work where the approving is the slow part, not the deciding.
argument-hint: "<ticket URL, defect id, or bug description>"
---

# /orbits-autopilot

Run this work on autopilot: $ARGUMENTS

## What autopilot is

It opens the gates it can defend on its own, takes its own recommended option, and keeps
going — then hands back with a record of every decision it made.

It does **not** remove the gates. It batches them: one review at the handover instead of five
conversations spread across a day. Every gate command still runs, every diff still gets read,
every finding still gets argued.

## How to run it

1. Load the `orbits` skill and read `references/autopilot.md` **first**, then each stage's
   section on entry.
2. Before starting, check the work against the good-fit / poor-fit table. If it is a poor fit,
   say so and recommend `/orbits` instead. Do not start a run you expect to abort.
3. Run **Overview → Resolve → Break down → Implement**, opening each gate yourself.
4. Write a decision-log entry for **every** gate you open. A gate opened without an entry was
   skipped, not automated.
5. Stop at **Test**. Hand back with the full decision log and the manual test script.
6. **Ship never runs on autopilot.** It leaves the machine.

## Hard stops — announce and wait

When one of these fires, say which one, state what you would have chosen, and stop:

- No baseline number and the change alters behaviour
- The evidence contradicts the ticket
- An abort condition fires — already fixed, not worth the cost, another system's problem
- Two approaches score within a hair of each other
- The change is one-way: a migration, a stored format, data already on people's devices
- It touches auth, payments, personal data, deletion, release or signing
- Blast radius is HIGH or CRITICAL
- A chunk fails twice
- A finding is still contested after two rounds
- The change reaches into a submodule or generated code
- Permissions are needed that the pre-flight did not anticipate
- Anything that leaves the machine: push, PR, ticket writes, deploys, messages

If hard stops are firing often, the task was not routine and this was the wrong mode. Say that
plainly.

## Handover shape

```
RAN            Overview → Resolve → Break down → Implement
DECISION LOG   one entry per gate opened
STOPPED AT     Test — needs a person holding a device
TEST SCRIPT    build · path · before · after · setup · watch
OPEN QUESTIONS anything a hard stop parked
UNDO           how to reverse the whole run
```
