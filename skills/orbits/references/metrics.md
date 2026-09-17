# The number

Overview records where the problem started. Resolve says what should change. Ship files a
ticket that goes and checks.

## The three shapes

```
BASELINE  recorded at Overview
  metric      crash-free sessions on the checkout screen
  query       <the exact query — it has to be re-runnable>
  value       97.1%
  date        2026-09-01
  version     12.3

TARGET    agreed at Resolve
  target      above 99.5%
  check at    12.4, once adoption passes 40%
  failure     still below 98%, or crashes move to another screen

FOLLOW-UP filed at Ship
  claim       what this change was supposed to fix
  owner       a named person, not a team
  trigger     a condition — adoption threshold, error volume, a release tag
  links       the PR, the original ticket, the defect
  if not met  who to tell, and what the next move is
```

The query matters more than the value. A value with no re-runnable query cannot be compared
to anything later, which means the orbit cannot close.

## Trailing and leading numbers

A fix has a **trailing** number: the thing was already happening and you measured it before
touching anything. New work has a **leading** number: nothing has happened yet, so you define
what success will look like and measure it after.

| Kind of work | The number |
|---|---|
| Crash, regression, defect | Occurrences, affected users, crash-free rate — measured before |
| Performance | The timing or resource figure, on a named path — measured before |
| New feature | Adoption of the new path, completion rate of the flow it sits in, time to first success |
| Replacement | Traffic moved off the old path, support contacts about the thing it replaces |
| Refactor with no user-visible change | Say so, and name the regret condition instead |

"No baseline" is an honest answer for a fix. It is rarely the honest answer for a feature — it
usually means nobody has decided what success looks like, which is worth catching at Overview.

## When there is genuinely no number

- Say so explicitly, in the problem statement.
- Name what will be watched after release instead, and how.
- Name the **regret condition**: what would make you wish you had not done this. A change
  nobody can name one for is a change nobody can evaluate.
- If the change alters behaviour and there is still no number, that is a **hard stop** on
  autopilot — the person decides whether to proceed blind.

## When to check

Schedule the check for when enough people are actually running the release — most crash tools
report version adoption, so use that as the trigger rather than a guessed date. Comparing too
early produces a confident wrong answer.

## Re-running it

Re-run the **identical** query. Three outcomes, all useful:

| Outcome | What it means | What happens |
|---|---|---|
| Moved as expected | The fix worked | Close it, and say so on the original ticket. This is how a team learns which fixes actually work. |
| Did not move | Wrong, incomplete, or aimed at the wrong cause | Reopen at **Overview** — now with better data than the first time. |
| Moved, something else worse | The negative check earned its keep | New problem, new pass. Better found by you than by a user. |

The negative check — "what would say it did *not* work" — is the one people leave out. It is
what catches a fix that moved its own metric by pushing the cost somewhere else.

## A follow-up that was never run is itself a finding

The follow-up is a ticket whose entire job is to ask an uncomfortable question about work
already marked done. Those are the first tickets to rot in any backlog.

So when the check did not happen, report that as the outcome — do not let it pass as silence.
A flow that quietly drops its own closing step is worse than one that never promised it,
because everyone involved believes the number was checked.

If it keeps happening, the flow is being performed rather than used. The honest metric for
that is **orbit closure rate**: of the runs that filed a follow-up, what share actually got
checked.
