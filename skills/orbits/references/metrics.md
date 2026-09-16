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
  links       the PR, the original ticket, the defect
  if not met  who to tell, and what the next move is
```

The query matters more than the value. A value with no re-runnable query cannot be compared
to anything later, which means the orbit cannot close.

## When there is no number

"No baseline" is an honest answer. Silence is not. When no number exists:

- Say so explicitly, in the problem statement.
- Name what will be watched after release instead, and how.
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
