# Output shapes

Fixed shapes per stage. No prose padding, no restating what just happened.

---

## Problem statement — end of Overview

```
PROBLEM     one sentence, in plain English
EVIDENCE    the primary records read, cited by path/id — not pasted
CAUSE       confirmed against the code, or "claimed, unconfirmed"
BASELINE    metric / query / value / date / version — or a reasoned "none available"
SCOPE       who is affected, on what versions, since when
GATE        the problem statement is agreed → waiting
```

---

## Approach options — end of Resolve

```
OPTION A    name
  cost      files touched · blast radius · migration · reversibility · fit
  for       …
  against   …
OPTION B    …
RECOMMEND   A, because …
TARGET      what moves, by how much, checked when, and what says it did NOT work
METHOD      test-first | follow-the-neighbour | design-first | model-first | measure-first
GATE        one approach and the target metric agreed → waiting
```

Record the rejected options in the ticket. That list ages well.

---

## Plan — end of Break down

```
BLAST RADIUS   LOW | MEDIUM | HIGH | CRITICAL, and why
EXISTING ISSUES
  path:line    problem → FIX NOW | TICKET | NOTE      (default TICKET)
SIMPLICITY     fewer files? abstraction used once? would the boring version work?
CHUNKS
  1  name      ≤3 files · gate command · acceptance criteria      (riskiest first)
  2  …
PERMISSIONS    see permissions.md pre-flight shape
PR WILL SHOW   the evidence decided now, not at Ship
GATE           plan approved and permissions cleared → waiting
```

---

## Implementer brief — one per chunk

Self-contained. Assume no memory of the repo. Paste the source material; do not link it.

```markdown
## Chunk N — <name>

### What to build
<one paragraph, plain English>

### Source material
<the ticket text, the defect detail, the design spec, decisions already made — pasted>

### Files
<the ≤3 files, with paths>

### Conventions to follow
<how the neighbouring code wires dependencies, names things, writes its tests —
 cited by path:line, not pasted wholesale>

### Acceptance criteria
- [ ] …
- [ ] …

### Gate command
<the exact command that must pass>

### Authorisation
You are authorised to make these changes now. Do not reply with a design and ask
whether to proceed — the plan is already approved. You may argue with the requirement
if the source material contradicts it; say so and stop rather than building the wrong
thing. Do not commit. Do not push.

### Effort
<cheap for mechanical work · expensive for concurrency, migrations, data formats>
```

---

## Chunk review — after each diff

```
CHUNK       N — name
DIFF        read · files touched
GATE RUN    the command, run first-hand · the real numbers
CRITERIA    each one → met | not met
FINDINGS    claim + evidence → fixed | defended (and dropped) | contested (round 1 of 2)
VERDICT     green → next chunk · red → round 2 · red twice → back to Break down
```

---

## PR body

One screen or less. Simple English. Design notes collapsed.

```markdown
## What this changes
<two or three sentences>

## Why
<the problem, with the baseline number>

## Proof
| Before | After |
|---|---|
| ![before](…) | ![after](…) |

## How it was verified
- <gate command> — <real numbers>
- Manual: <the script the person ran>

<details>
<summary>Design notes</summary>

<the trade-offs, the rejected options, the existing issues filed as tickets>

</details>

Fixes #<ticket>
Follow-up: #<the check-the-number ticket>
```

---

## Follow-up ticket — filed at Ship

```
TITLE       Check: did <metric> move after <change>?
CLAIM       what this change was supposed to fix
QUERY       the exact re-runnable query from the baseline
BASELINE    value / date / version
TARGET      the agreed target, and the failure condition
CHECK WHEN  version <n> once adoption passes <x>%
LINKS       the PR · the original ticket · the defect
IF NOT MET  who to tell, and what the next move is
```

---

## Decision log entry — autopilot only

```
GATE        which gate, and when
CHOSE       what it picked
BECAUSE     the reason, one line
REJECTED    what it did not pick, and why
CONFIDENCE  high | medium
UNDO        how to reverse this if you disagree
```
