---
"mattpocock-skills": patch
---

Expand `testing` to cover the shape of the suite, not only the quality of a single test.

- Require a contiguous three-line `Given`, `When`, `Then` comment block at the top of every test body, briefly stating that test's setup, observed action, and expected behaviour. Reusable boilerplate, restating the test name, annotating every line, and vague phrases such as "the described behavior" are called out as failures.
- Update the `tests.md` `GOOD` examples to show the block, so the authoritative examples no longer contradict the rule. This is the one place `testing/tests.md` deliberately diverges from `tdd/tests.md`, since only `testing` mandates the block.
- Add a **Directory and file organization** section: respect the repository's test discovery first, group by feature and observable behaviour at the agreed seams, keep the hierarchy shallow and meaningful, give each file a coherent review topic, make execution requirements (deterministic behaviour, adapters against real resources, end-to-end) discoverable through directories, suites, or tags, scope support code to its consumers, and keep physical layout separate from execution grouping.
- Widen the description to cover reviewing and organising an existing suite, not only writing new tests. `README.md`, `skills/engineering/README.md`, `docs/engineering/testing.md`, `ask-matt`, and `docs/engineering/ask-matt.md` are re-synced to match.
