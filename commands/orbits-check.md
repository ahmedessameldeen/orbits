---
name: orbits-check
description: Close the orbit — re-run the baseline query weeks after a fix shipped and find out whether the number actually moved. The step almost every team skips.
argument-hint: "<the follow-up ticket, PR, or the baseline metric>"
---

# /orbits-check

Close the orbit on: $ARGUMENTS

**A merged pull request is a claim, not evidence.** The evidence arrives weeks later, in the
data.

## How to run it

Load the `orbits` skill and read `references/metrics.md`.

1. **Find the baseline.** Read the run file — metric, exact query, value, date, version were
   recorded at Overview. If there is no run file and no recorded query, say so plainly: this
   check cannot be completed, and that is a finding about the process, not about the fix.
2. **Check the timing first.** Has the release reached real adoption? Most crash tools report
   version adoption — use that as the trigger rather than a guessed date. Comparing too early
   produces a confident wrong answer. If it is too early, say when to come back.
3. **Re-run the identical query.** Not a similar one. Not a better one.
4. **Check the failure condition too** — the "what would say it did *not* work" agreed at
   Resolve. This is what catches a fix that moved its own metric by pushing the cost somewhere
   else.

## Report the outcome

| Outcome | What happens |
|---|---|
| Moved as expected | Close it, and say so on the original ticket. This is how a team learns which fixes actually work. |
| Did not move | Reopen at **Overview** — now with better data than the first time. |
| Moved, something else worse | New problem, new pass. Better found by you than by a user. |

## Output shape

```
BASELINE    metric / query / value / date / version
NOW         the same query, re-run · value / date / version
ADOPTION    what share of users are on the release
TARGET      agreed at Resolve · met | not met
NEGATIVE    the failure condition · triggered | clear
OUTCOME     moved | did not move | moved, something else worse
NEXT        close it · reopen at Overview · new pass
```

Whatever the result, write it back onto the original ticket and into the run file. An
unrecorded outcome teaches nobody anything.

**If the check was never run until now**, say that too. A follow-up that sat unopened past its
trigger is itself a finding — the flow quietly dropped its own closing step while everyone
involved believed the number had been checked.
