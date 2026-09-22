---
name: testing
description: Testing guidance for features and bug fixes. Use when the user wants durable automated or integration tests through public interfaces, or to review and organize a test suite.
---

# Testing

This skill is the reference for producing tests worth keeping: what a good test is, where tests go, and the anti-patterns. Consult it before and during implementation so tests and code can inform each other.

When exploring the codebase, read `CONTEXT.md` (if it exists) so test names and interface vocabulary match the project's domain language, and respect ADRs in the area you're touching.

## What a good test is

Tests verify behavior through public interfaces, not implementation details. Code can change entirely; tests shouldn't. A good test reads like a specification — "user can checkout with valid cart" tells you exactly what capability exists — and survives refactors because it doesn't care about internal structure.

At the beginning of each test body, place a contiguous three-line `Given`, `When`, and `Then` comment block that briefly states that test's specific setup, observed action, and expected behavior. A reader should understand the scenario from this block without reading the code. Do not use reusable boilerplate, merely repeat the test name, annotate every test line, or hide important conditions behind vague phrases such as "the described behavior."

See [tests.md](tests.md) for examples and [mocking.md](mocking.md) for mocking guidelines.

## Seams — where tests go

A **seam** is the public boundary you test at: the interface where you observe behavior without reaching inside. Tests live at seams, never against internals.

**Test only at pre-agreed seams.** Before writing any test, write down the seams under test and confirm them with the user. No test is written at an unconfirmed seam. You can't test everything — agreeing the seams up front is how testing effort lands on the critical paths and complex logic instead of every edge case.

Ask: "What's the public interface, and which seams should we test?"

When the shape of that interface is itself in question — how deep the module is, where the seam belongs, what the interface should expose — call the Skill tool with "codebase-design" for the vocabulary. It is the shared source of the module, interface, depth, seam, adapter, leverage and locality terms, and it is a reference to consult, not a session to run.

## Directory and file organization

Organize tests so a reviewer can find a capability, understand its scenarios, and identify the boundary being exercised without knowing the implementation's class hierarchy.

- **Respect test discovery first.** Use the repository's existing test roots, framework conventions, and naming rules. Within them, group by feature and observable behavior at the agreed seams. Do not mechanically mirror implementation layers or create a test file for every internal class.
- **Keep the hierarchy shallow and meaningful.** A small suite can stay flat. Introduce a directory when it groups a recognizable responsibility or separates tests with different execution needs. Do not create empty categories, mandatory layer trees, or separate targets solely for visual tidiness.
- **Give each file a coherent review topic.** Split when unrelated behaviors require independent review or setup obscures the scenarios; do not impose an arbitrary line limit or one-test-per-file rule. Name files and directories after the actual behavior or boundary under test. Moving an internal executor test into a controller directory does not turn it into a public-interface test.
- **Make execution requirements discoverable.** Distinguish deterministic behavior tests, tests of adapters using real resources, and end-to-end integration tests where they exist. Use the repository's directories, suites, or tags rather than requiring all three categories everywhere. A reviewer should be able to tell which tests need devices, models, network access, or other external resources and how to run them.
- **Scope support code to its consumers.** Keep single-file helpers local. Put genuinely shared fixtures, fakes, and synchronization helpers in a nearby `Support` directory or the repository's equivalent; use a common root only for helpers shared across features. Support code must not duplicate business logic, hide important event ordering or assertions, or grow into a universal fixture with unrelated switches.
- **Separate physical layout from execution grouping.** Splitting files does not require splitting logical suites. Preserve isolation or serialization for tests sharing process-wide or device resources, even across directories. Never depend on test execution order or assume separate files cannot run concurrently.

## Anti-patterns

- **Implementation-coupled** — mocks internal collaborators, tests private methods, or verifies through a side channel (querying the database instead of using the interface). The tell: the test breaks when you refactor but behavior hasn't changed.
- **Tautological** — the assertion recomputes the expected value the way the code does (`expect(add(a, b)).toBe(a + b)`, a snapshot derived by hand the same way, a constant asserted equal to itself), so it passes by construction and can never disagree with the code. Expected values must come from an independent source of truth — a known-good literal, a worked example, the spec.
- **Horizontal slicing** — separating all tests from all implementation. Bulk tests verify _imagined_ behavior: you test the _shape_ of things rather than user-facing behavior, the tests go insensitive to real changes, and you commit to test structure before understanding the implementation. Work in **vertical slices** instead — keep one observable behavior, its test, and its implementation together, then repeat. Each slice is a **tracer bullet** that responds to what the last slice taught you.
