## What it does

`code-review-loop` repeatedly reviews a branch against its standards and originating [spec](https://www.aihero.dev/ai-coding-dictionary/spec), fixes confirmed findings, and runs another review when the findings justify it. Standards and spec reviewers work independently, and each round starts with fresh reviewers who do not see earlier findings or fixes.

A round stops only after there are no findings or only low-severity findings remain. All confirmed findings, including low-severity ones, are fixed before it stops.

## When to reach for it

In Codex, invoke `/code-review-loop` explicitly when you want an iterative review and fix loop.

| Your situation | Reach for |
| --- | --- |
| You want confirmed review findings fixed and checked in fresh rounds until the review converges | `/code-review-loop` |
| You want one review pass and a findings report | [code-review](https://aihero.dev/skills-code-review) |
| You want implementation notes, iterative fixes, and a pull request as one workflow | [implement-loop](https://aihero.dev/skills-implement-loop) |

## Prerequisites

The review needs a clear starting commit. The originating spec and repository standards should be available so findings can be checked against the work's intent.

## Review rounds

The loop keeps standards findings separate from spec findings. Prior review history is withheld from the next round, which lets the new reviewers assess the current branch independently.

## Common questions

**Why does every round use fresh reviewers?**

A fresh review avoids anchoring on earlier findings, discussion, or fixes. Each round judges the current branch against the same sources.

**Does it stop after high and medium findings are fixed?**

No. Every confirmed finding is fixed, including low-severity findings. A new round is needed after a round with confirmed high- or medium-severity findings.

## It's working if

- Each round has independent standards and spec findings.
- Confirmed findings are resolved before another round starts.
- The loop stops after a clean round or a round with only low-severity findings.

## Where it fits

`code-review-loop` is an iterative review and fix step after implementation, while [code-review](https://aihero.dev/skills-code-review) runs a single review pass. It is part of [implement-loop](https://aihero.dev/skills-implement-loop)'s build workflow and can also be reached on its own. [ask-matt](https://aihero.dev/skills-ask-matt) routes you through the full set.
