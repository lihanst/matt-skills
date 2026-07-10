---
name: implement-loop
description: "Implement a piece of work based on a spec or set of tickets."
---

Implement the work described by the user in the spec or tickets.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, loop: run /code-review, fix every finding that is not low severity, and repeat until the only remaining issues are low severity.

Commit your work to the current branch.
