## What it does

`implement-loop` carries an agreed [spec](https://www.aihero.dev/ai-coding-dictionary/spec) or [ticket](https://www.aihero.dev/ai-coding-dictionary/ticket) through implementation, review, and a pull request while keeping a running record of decisions and deviations. The notes are stored under `~/CodexScratch/<repo>/<branch>/` and updated as each decision happens, so the final description can explain changes from the spec.

The notes are written as the work unfolds, not reconstructed from memory at the end.

## When to reach for it

In Codex, invoke `/implement-loop` explicitly to start the implementation, review, and publishing workflow.

| Your situation | Reach for |
| --- | --- |
| You want a spec or ticket implemented, decision notes kept, review findings fixed in rounds, and a pull request opened | `/implement-loop` |
| You want the parallel frontier of a ticket graph built on one integration branch | [implement-spec](https://aihero.dev/skills-implement-spec) |
| You want to implement one ticket in a fresh session and handle publishing yourself | [implement](https://aihero.dev/skills-implement) |

## Prerequisites

The spec or ticket must be ready to implement. If the work is in an issue tracker, configure the tracker first. The run commits, pushes, and opens a pull request, so the repository needs a writable remote.

## Implementation notes

The notes preserve decisions the spec left open, deviations and their reasons, trade-offs, and deferred work. If they contain a Deviations section, that section is included in the pull request description.

## Common questions

**Where do the notes go?**

They are kept under `~/CodexScratch/<repo>/<branch>/`, with one directory per repository and branch.

**Does it open a pull request automatically?**

Yes. The run commits and pushes its branch, then opens a pull request. If the notes contain a Deviations section, that section is copied into the pull request description.

## It's working if

- The notes file records decisions while they happen.
- Any departure from the spec has a reason in the notes and is visible in the pull request description.
- Review findings are fixed across review rounds before the pull request is opened.

## Where it fits

`implement-loop` is an end-to-end build path after [to-tickets](https://aihero.dev/skills-to-tickets):

`grill-with-docs` → `to-spec` → `to-tickets` → `implement-loop`

Use [implement](https://aihero.dev/skills-implement) for one ticket at a time, and [implement-spec](https://aihero.dev/skills-implement-spec) to run the ready ticket frontier in parallel. [code-review-loop](https://aihero.dev/skills-code-review-loop) gives implement-loop its repeated review and fix rounds. [ask-matt](https://aihero.dev/skills-ask-matt) routes you through the full set.
