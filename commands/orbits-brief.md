---
name: orbits-brief
description: Write a self-contained implementer brief for one chunk of an approved ORBITS plan — with the source material pasted in, acceptance criteria, a gate command, and standing authorisation.
argument-hint: "<chunk number or name>"
---

# /orbits-brief

Write the implementer brief for: $ARGUMENTS

If no chunk was named, list the chunks from the approved plan and ask which one. If there is
no approved plan, stop — briefing before Break down is how an implementer ends up inventing
the requirement.

## The two rules that make a brief work

**Context parity.** The implementer gets the same material the orchestrator has — ticket text,
defect detail, design spec, decisions already made — **pasted into the brief, not linked**. An
implementer without the ticket invents a requirement. One that has it can argue with it, and
that argument is worth having. Where the agent cannot reach a source, carry the content
across yourself.

**Standing authorisation.** Include it explicitly, or the reply comes back as a design and the
question "shall I proceed?". Break down was the planning; the brief is the approval.

## How to run it

Load the `orbits` skill and read `references/templates.md` for the brief shape.

1. One chunk per brief. Three files or fewer. Riskiest chunk first.
2. Self-contained — assume no memory of the repo.
3. Cite conventions by `path:line`; do not paste whole files. Cheap for you, cheap for them.
4. Dial effort per chunk, not per task: cheap for mechanical work, expensive for concurrency,
   migrations and stored data formats.
5. State plainly: **do not commit, do not push.**
6. Give the exact gate command that must pass.

## After the brief comes back

Review the diff against **that chunk's** criteria and run **that chunk's** gate first-hand,
before the next chunk begins. Findings get fixed *or defended* — when a defence is right, drop
the finding and say so plainly.

Two failures on one chunk means the plan was wrong. Go back to Break down. Do not grind.
