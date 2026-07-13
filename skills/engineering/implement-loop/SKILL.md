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

Store the notes under `~/CodexScratch/<repo>/<branch>/`.

Update the notes when each decision occurs, not retrospectively at the end

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once implementation is done, follow /code-review-loop until the review passes.

Commit and push your work, then create a pull request. If the implementation notes contain a `Deviations` section, include that section in the pull request description.
