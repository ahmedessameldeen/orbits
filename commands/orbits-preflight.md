---
name: orbits-preflight
description: Clear the permissions an ORBITS run needs before Implement starts, so the chunk loop runs without approval prompts — while leaving the sharp ones prompting.
argument-hint: "[the approved plan, or the files and gate commands it names]"
---

# /orbits-preflight

Run the permission pre-flight for: $ARGUMENTS

If no plan was given, use the plan from the current run's Break down stage. If there isn't
one, say so — the pre-flight is predicted *from* the plan, and guessing without it produces
exactly the bloated allowlist this is meant to avoid.

## How to run it

Load the `orbits` skill and read `references/permissions.md`.

1. **Read what is already cleared** in the project's shared settings. Do not re-add it.
2. **Predict only what is new** from the plan: a module not built before, a service read for
   the first time, a scratch path being written to.
3. **Write patterns, not literals.** An entry naming one exact test invocation matches once
   and never again. That is the actual cause of prompt fatigue — not missing pre-approval.
4. **Clear both surfaces.** The orchestrator has its own permissions; a delegated implementer
   in its own sandbox has separate ones — approval mode, trusted-project list, write policy.
   A pre-flight that clears only the first still stalls on the second.
5. **Leave the sharp ones prompting** and name them, so nobody is surprised mid-run.

## Audit this every time

Broad wildcards over the version-control CLI usually swallow push and pull-request creation
without anyone noticing. Check for them. Without that check, "only push when asked" is
enforced by nothing but good manners.

## Output shape

```
ALREADY CLEARED   what the project settings already cover
NEW THIS TASK     the specific additions this plan needs, in general form
SECOND SURFACE    what the delegated implementer needs, separately
LEFT PROMPTING    push · PR open/merge · force-push · deletes · deploy · secrets
WILDCARD AUDIT    any broad pattern found, and what it silently allows
```
