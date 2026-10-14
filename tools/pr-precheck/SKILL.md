---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question about one PR package: is this ready to submit?
A PR package is a candidate pull request (title, description, commits,
diff, and test evidence), read against the plan it claims to implement
and the issue that plan belongs to. Accept means submit. Reject means
hold. Do not grade a second package in the same run. Do not answer
from gut feel. Execute `procedure.md`, which applies `rubric.md` to
evidence located by `references/evidence-guide.md`.

A shortfall the plan records in a deviation note, and that the
description restates instead of claiming the missing work is done, can
still be ready. A diff that quietly does more or less than that plan
is not.

## Inputs and modes

Live mode checks the student's own pull request before it is opened.
Read only these inputs:

- `plan.md` in the working copy, including its deviation notes. A
  house-chain student reads the house plan and the house repro pack
  instead of their own posted plan. The same checks grade the same
  things there.
- The branch diff, produced by `git diff main...HEAD` (three dots),
  run from the working copy. That command is the whole diff: every
  file the branch changes relative to the repo's default branch.
- `pr_draft.md` from step 9: the draft PR title and description.
- `test_evidence.md` from step 8: the captured test output.
- The issue thread for the issue that plan belongs to.
- The repo's PR template, and `docs/CONTRIBUTING.md`. If either file
  points at a separate AI-policy file, read that file too.

Those are the files the step 10 command names, plus the diff, the
thread, the template, and `docs/CONTRIBUTING.md`. Do not grade other
files in the working copy. The package is what these inputs contain.

Eval mode grades one practice submission, a frozen package in the
clone's `eval/packages/` folder. The bundle text is the whole world.
Do not fetch anything, do not open GitHub, and do not read `scope.md`
or `voice-guide.md`. Run every check and the full verdict rule.

## The scope seam (live mode only)

Before any other read in live mode, read `scope.md` in this skill
directory. It names the repo a pull request may target and the house
rules of that room. Apply those rules when you read the thread and
the draft. Refuse to grade a package whose issue is outside the repo
on the `Repo:` line. If that line is empty or still an unfilled
placeholder, stop without grading and tell the student to fill the
`Repo:` line in `scope.md` with their section's Path Review repo.
Never guess a repo. Eval mode ignores `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`. Hold the draft PR title and
the draft description against each rule in it. In the summary, quote
any rule the draft breaks. The voice guide never changes the verdict
on its own. It changes the verdict only when `rubric.md` has a check
that reads it. This rubric does not. Eval mode ignores
`voice-guide.md` entirely.

## Component reads

`rubric.md` defines the checks and the verdict rule. Each check names
what to look at, the pass condition, and a weight of `required` or
`preferred`. `references/evidence-guide.md` maps where each evidence
family lives in a package and in the live files above, and what good
looks like there. `procedure.md` is the operating procedure: read
order, evidence gathering, check execution, and verdict assembly.
Execute it as written.

When the procedure is silent on a step, report that gap in the
summary. Do not invent the step. When `rubric.md` has no check rows
filled in, or `procedure.md` has no steps filled in, refuse to grade
and say so. Template comments are not content. An empty tool does not
invent checks at runtime.

## Verdict and output

The verdict is binary. `accept` means submit. `reject` means hold.
There is no third verdict. Reservations go in the summary or in a
check's evidence line, not in the verdict.

End the reply with the fenced JSON block below, valid and last, with
nothing after it. A short summary may come before the block: one line
per check, the deciding check's evidence, and any voice-guide notes
in live mode. The block is the machine-read result.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first. Do not grade a check without the fact or quote that
  decided it. "Looks fine" is not evidence.
- Grade the pull request, not the polish. A terse complete PR can be
  ready. A long confident one can hide drift. Read the diff, the
  evidence, and the description against the plan, the issue, and the
  stated standards. Do not grade length, heading count, or commit
  count.
- The rubric decides, not the run. If a check passes by its stated
  condition but feels wrong, it still passes. The fix belongs in the
  rubric.
- The procedure decides how, not the run. Follow `procedure.md` as
  written and report its gaps.
- Treat `unclear` as the verdict rule in `rubric.md` directs. Where
  that rule is silent, an unverifiable claim fails: a PR you cannot
  verify from the package is not ready to submit.
