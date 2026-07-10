---
name: code-review-loop
description: Repeatedly review and fix changes against repository standards and an originating spec until every confirmed finding is low severity.
---

Run a convergent review-fix loop. The user must invoke this skill explicitly.

## Review protocol

Read `../code-review/SKILL.md` before starting. Reuse its fixed-point, spec-source, standards-source, smell-baseline, and two-axis review rules as the rubric for each round. Do not modify that skill.

Classify every finding as:

- **High** — correctness, security, data-loss, or major spec-compliance risk.
- **Medium** — a concrete reliability, test, or maintainability problem with credible impact.
- **Low** — optional polish, minor style, or low-risk improvement.

## Loop

1. Pin the fixed point and collect the spec and standards sources using the `code-review` protocol.
2. Spawn the Standards and Spec reviewers in parallel. Every round must use fresh, read-only sub-agents with `fork_turns="none"`.
3. Give each reviewer only the total review scope and the material needed for its axis. Do not reveal the current round, prior findings, prior discussions, fixes already made, or the parent's opinion.
4. Include these instructions verbatim in every reviewer prompt:

   > Work as a read-only reviewer. Do not edit files, commit, push, or change repository state. Do not load or invoke the code-review skill. Do not spawn sub-agents. Review only the supplied scope and evidence. Assign High, Medium, or Low severity to every finding.

5. After spawning the reviewers, wait quietly for every result. Do not interrupt them, modify code, or do unrelated work while they run.
6. Assess every finding against the diff, standards, and spec. If you disagree, send the objection to the same reviewer and continue the discussion until the reviewer either withdraws the finding or both sides agree on its wording and severity. Do not fix anything while a disagreement remains unresolved.
7. Once all disagreements are resolved, fix every confirmed High and Medium finding. Leave Low findings unchanged unless the user explicitly asks for them.
8. Run the checks relevant to the fixes.
9. Start another round with entirely new reviewers. Give them the same clean scope and source material, with no review history.
10. Stop only when there are no confirmed High or Medium findings.

At the end, report the number of rounds, the confirmed findings fixed, validation results, and any remaining Low findings. Do not commit unless the user's request or another explicitly invoked skill requires it.
