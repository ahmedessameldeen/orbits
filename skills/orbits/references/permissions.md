# No interruptions during Implement

Every approval prompt mid-implementation breaks the loop, costs a context switch, and tempts
everyone toward a blanket "allow everything" that removes the prompts worth keeping.

Pre-approving is the right instinct. But the usual cause of prompt fatigue is not missing
pre-approval — it is an allowlist built from **literal one-off commands instead of patterns**.
An entry naming one exact test invocation matches once and never again. Ten near-identical
entries pile up, the list grows to hundreds of lines, and the prompts keep coming.
Generalising is what fixes it.

## Two surfaces, not one

The orchestrator has its own permissions. A delegated implementer running in its own sandbox
has separate ones — an approval mode, a trusted-project list, a write policy. A pre-flight that
clears only the first still stalls on the second. Clear both.

## Once per project

Write generalised patterns into the project's shared settings so the whole team benefits:

- the build tool, in general form — not one exact invocation
- read-only inspection commands
- the test toolchain
- device tooling
- the analytics and design services the flow reads from

## Once per task, at Break down

The plan already names the files and the gates. From it, predict only what is **new**:

- a module not built before
- a service read for the first time
- a scratch path being written to

Two minutes here buys an uninterrupted run.

## Leave the sharp ones prompting

Push, open or merge a PR, force-push, delete branches or files, deploy, anything touching
production or secrets.

These prompts are not friction — they are the last checkpoint before an action that leaves the
machine.

**Audit broad wildcards over your version-control CLI.** They usually swallow push and PR
creation without anyone noticing, which quietly turns "only push when asked" into a rule
enforced by nothing but good manners.

## Pre-flight output shape

```
ALREADY CLEARED   what the project settings already cover
NEW THIS TASK     the specific additions this plan needs, in general form
SECOND SURFACE    what the delegated implementer needs, separately
LEFT PROMPTING    the sharp ones, named, so nobody is surprised
```
