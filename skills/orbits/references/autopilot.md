# Autopilot

A mode for when the approving is the slow part, not the deciding.

**Autopilot flies the cruise, not the landing.** It opens the gates it can defend on its own,
takes its own recommended option, and keeps going — then hands back with a record of every
decision it made for you.

It does not remove the gates. It **batches** them: one review at the handover instead of five
conversations spread across a day. The quality bar does not move — every gate command still
runs, every diff still gets read, every finding still gets argued.

## What it covers

```
┌─ AUTOPILOT — GATES SELF-OPENED, EACH ONE LOGGED ─┐   ┌─ PERSON HAS THE CONTROLS ─┐
│  Overview ─► Resolve ─► Break down ─► Implement  │──►│      Test ─► Ship         │
└──────────────────────────────────────────────────┘   └───────────────────────────┘
                                          handover      needs a person   leaves the
                                                        holding a device machine —
                                                                         cannot be
                                                                         quietly undone
```

The two gates autopilot never opens are not policy choices. Test needs a person holding a
device; Ship sends work somewhere it cannot be quietly retrieved from. Everything before them
is where the waiting actually lives.

## Hard stops — in every mode

Each is a case where guessing wrong is expensive and the person knows something the flow does
not. When one fires, say **which**, state what you **would have chosen**, and wait.

**About the problem**
No baseline number and the change alters behaviour · the evidence contradicts the ticket · an
abort condition fires — already fixed, not worth the cost, belongs to another system.

**About the approach**
Two approaches score within a hair of each other · the change is one-way — a migration, a
stored format, data already on people's devices · it touches auth, payments, personal data,
deletion, release or signing · blast radius is HIGH or CRITICAL.

**About the work**
A chunk fails twice — a wrong plan does not improve by being retried harder · a finding is
still contested after two rounds · the change reaches into a submodule or generated code ·
permissions are needed that the pre-flight did not anticipate.

**Always**
Anything that leaves the machine: push, pull request, ticket writes, deploys, messages.

## The decision log

What makes autopilot reviewable rather than merely fast. Every gate it opens on your behalf
gets one entry.

```
GATE        which gate, and when
CHOSE       what it picked
BECAUSE     the reason, one line
REJECTED    what it did not pick, and why
CONFIDENCE  high | medium — anything lower is a hard stop, not a log entry
UNDO        how to reverse this if you disagree
```

**A gate opened without an entry was skipped, not automated.**

## When to use it

| Good fit | Poor fit |
|---|---|
| A well-specified bug with a clear reproduction and a real number behind it. A mechanical refactor with strong coverage. A dependency bump. Anything where you would have approved the obvious plan anyway. | Anything where the requirement is genuinely uncertain, where you would want to argue about the approach, or where being wrong is expensive to unwind. Those are the tasks the gates exist for. |

Said plainly: autopilot is a bet that the recommended option is right. It pays off on routine
work and costs a whole run on ambiguous work. The hard-stop list is what keeps the bet small —
**if it is firing often, the task was not routine and the mode was the wrong choice.**
