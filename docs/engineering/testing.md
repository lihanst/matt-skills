## What it does

`testing` is the general reference for tests worth keeping: public interfaces, agreed test seams, vertical slices, independent expected values, and mocks at system boundaries.

It deliberately leaves the order of tests and implementation open. The implementation and tests should inform each other within the same observable-behaviour slice, but the skill does not prescribe which one comes first.

## When to reach for it

Type `/testing`, or the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) reaches for it automatically when a task needs automated or integration tests without a prescribed test-first workflow.

| Your situation | Where to go |
| --- | --- |
| You want durable tests and the agent may choose the test timing | `testing` |
| You explicitly want test-first or red-green | [tdd](https://aihero.dev/skills-tdd) |
| The behaviour is not settled yet | [to-spec](https://aihero.dev/skills-to-spec) |
| The open question is the shape of the interface | [codebase-design](https://aihero.dev/skills-codebase-design) |
| You have a full spec or set of tickets to build | [implement](https://aihero.dev/skills-implement), which drives this skill internally |

## Prerequisites

[codebase-design](https://aihero.dev/skills-codebase-design) needs to be installed because it owns the interface and seam vocabulary this skill consults. Nothing else; the skill is [stateless](https://www.aihero.dev/ai-coding-dictionary/stateless) and writes no files of its own.

## Flexible timing at a pre-agreed seam

A **seam** is the public boundary where behaviour can be observed without reaching into internals. Testing effort is finite, so the skill names the seams it intends to test and confirms them with you before writing a test.

Within each seam, work stays vertical: one observable behaviour, its implementation and tests, then the next behaviour. The test can arrive at any point inside that slice. The opposite is horizontal slicing, where implementation and tests land as separate batches and stop informing each other.

The tests themselves follow three constraints:

- Verify behaviour through public interfaces, so internal refactors do not break them.
- Take expected values from an independent source such as a spec, worked example, or known literal.
- Mock system boundaries such as external APIs, time, or randomness, not internal collaborators.

## Common questions

**How is this different from `/tdd`?**

`tdd` requires the test to go red before implementation makes it green. `testing` lets the agent choose the order while preserving the same standards for seams and test quality. Use `tdd` when the order itself is part of what you want.

**Is it a problem if the implementation comes before the test?**

No. The useful signal is whether the test exercises observable behaviour and would detect a regression. The implementation and tests should still remain in the same vertical slice instead of arriving as separate batches.

**It asked me to choose a seam and I did not know which one to pick.**

Ask for the trade-offs between the candidates: what each seam catches, what it misses, and how expensive it is to run. This is also why the main flow agrees seams in [to-spec](https://aihero.dev/skills-to-spec), while the whole feature is still visible.

**Should browser or end-to-end tests be the first feedback loop?**

Usually not. They are often too slow and failure-prone to guide each implementation slice. Prefer a faster public boundary during the build, then add browser coverage once the behaviour works when the user-facing path warrants it.

## It's working if

- The intended test seams are named and confirmed before test files change.
- Implementation and tests stay together around one observable behaviour at a time.
- Test names read as capabilities, not internal call sequences.
- Renaming an internal function does not break the suite.
- Expected values trace to a spec or known example rather than recomputing the implementation.
- Mocks appear at external boundaries, not around the project's own modules.

## Where it fits

`testing` is the default testing reference inside [implement](https://aihero.dev/skills-implement). [tdd](https://aihero.dev/skills-tdd) is its test-first sibling, and [code-review](https://aihero.dev/skills-code-review) owns the review and refactoring stage after implementation. When you are unsure which skill fits, [ask-matt](https://aihero.dev/skills-ask-matt) routes you.
