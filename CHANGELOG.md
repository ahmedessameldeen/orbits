# Changelog

## 1.1.0

Integrates a pre-publication review of the flow. No new stages, no new commands.

### Fixed inconsistencies

- The banner said "agents never commit" while Ship said "commit and push only when the person
  asks". The rule is about the machine boundary, not the verb: **nothing leaves the machine
  without a person.**
- Added a gloss on *Resolve* — resolving on a course of action, not resolving the ticket.
- Added the third return path, **Break down → Overview**, for when the cause turns out to be
  elsewhere. Previously this was handled by silently rewriting the problem statement.

### Added

- **The run file.** One file per unit of work, updated at every gate, carrying the baseline,
  target, rejected options, chunk list, gates opened, rollout and follow-up. Makes a run
  survive a lost session, change hands, and close weeks later without archaeology.
- **Trailing and leading numbers.** New work has numbers too — adoption, completion rate, time
  to first success. "No baseline" is honest for a fix and rarely honest for a feature.
- **Regret condition** at Overview, for work where no number applies.
- **Rollout, kill switch and revert threshold** at Ship, covering the previously unmanaged gap
  between merge and evidence. The revert threshold asks *is this actively hurting*; the failure
  condition asks *did this work*.
- **Named owner and a condition trigger** on the follow-up. A follow-up that was never run is
  itself a finding, and **orbit closure rate** is the flow's own metric.
- **A new requirement is a new orbit**, as a standing rule.
- A definition of what counts as a **round** in "two rounds, then escalate".

### Docs

- README opens with the flow diagram — light and dark SVGs, switched by the reader's GitHub
  theme — plus a short guide to reading it.

### Generalised

- Test is now "a human exercises the change in a real environment", with a translation table
  for mobile, web, backend, library and data work. The flow was visibly mobile-shaped.

## 1.0.0

Initial release.
