---
name: implement-loop
description: "Implement a piece of work based on a spec or set of tickets."
---

Implement <SPEC> and, whilst you work, maintain a running
implementation-notes.html (or implementation-notes.md) that records:

- Decisions you made that were not spelled out in the spec
- Anything you changed relative to the spec and why
- Trade-offs, shortcuts, or deferred work
- Anything else the maintainer should know before shipping

Keep an `implementation-notes.md` file. If you hit an edge case that forces you to deviate from the plan, pick the conservative option, log it under `Deviations`, and keep going.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Require the user to invoke /code-review-loop alongside this skill. Once implementation is done, follow /code-review-loop until the only remaining findings are low severity.

Commit your work to the current branch.
