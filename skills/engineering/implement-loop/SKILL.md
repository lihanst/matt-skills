---
name: implement-loop
description: "Implement a piece of work based on a spec or set of tickets."
---

Implement the work described by the user in the spec or tickets.

Keep an `implementation-notes.md` file. If you hit an edge case that forces you to deviate from the plan, pick the conservative option, log it under `Deviations`, and keep going.

Also record decisions the spec did not make, trade-offs, and open questions under matching headings. Conservative means the smallest reversible choice that preserves existing behaviour and public interfaces without expanding scope. Do not pause to ask the user about implementation ambiguity; log the choice and continue. Do not put review-round history in this file.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Require the user to invoke /code-review-loop alongside this skill. Once implementation is done, follow /code-review-loop until the only remaining findings are low severity.

Commit your work to the current branch.
