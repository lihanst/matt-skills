---
name: implement-loop
description: "Implement a piece of work based on a spec or set of tickets."
---

Implement the work described by the user in the spec or tickets.

While implementing, keep a running `implementation-notes.md` file with decisions you had to make that were not in the spec, things you had to change, trade-offs you had to make, or anything else the user should know.

Keep an `implementation-notes.md` file. If you hit an edge case that forces you to deviate from the plan, pick the conservative option, log it under `Deviations`, and keep going.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Require the user to invoke /code-review-loop alongside this skill. Once implementation is done, follow /code-review-loop until the only remaining findings are low severity.

Commit your work to the current branch.
