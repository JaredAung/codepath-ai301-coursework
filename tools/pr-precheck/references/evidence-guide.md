# Evidence guide: where evidence lives in a PR package

The four headings below are the four ways a practice submission is held. Plan fidelity is silent drift. Test evidence is not tested. Diff quality is unreviewable. Standards and comms is the standards wall. A package that fails none of them is ready to submit, including one that does less than the issue because the plan's deviation note says so and the description restates that limit.

`calib-01` is the picture of ready: one deleted line in the file the plan names, a short description, and the parse error shown before and after. Use it as the shape of a pass. The locations below are the same sections every package has.

## Plan fidelity (harness category: silent-drift)

Used by `plan-fidelity`.

Where it lives:

- Eval: the scope pair in `## Plan context` (the in-scope change, the files it names, the not-in-scope line, and any sentence marked deviation, deferred, or known limit). Read that against `### Diff` (each `--- a/` file and what the hunk adds or removes) and against the fidelity sentences in `### Description` (what it says the PR changed, including "exactly", "in full", or "no other changes").
- Live: the same pair in `plan.md`, including its deviation notes. Read it against `git diff main...HEAD` from the working copy, and against the description in `pr_draft.md`.

What good looks like: every behavior the diff changes is the change the plan names, or a test, changelog, or docs file that plan or the template asks for. In `calib-01` the plan names `themes.gitconfig` and the deletion of the shadowed `file-decoration-style` line, and the diff is that one deletion. An honest shortfall is also a pass: the plan's note says the rest is deferred, and the description repeats that limit instead of claiming the missing work shipped. Silent drift is a diff that adds a file, option, or rewrite the plan never names and no note covers, or a description that claims a deliverable the diff does not contain.

## Test evidence (harness category: not-tested)

Used by `test-decisive`.

Where it lives:

- Eval: `### Test evidence`, read against the test-plan sentences in `## Plan context` (the command or scenario and the outcome, including a second failure mode when the plan names one) and against a test command named on the repo-facts pull-requests or contribution line.
- Live: `test_evidence.md` from step 8, read against the test plan in `plan.md` and against a test command named in `docs/CONTRIBUTING.md`.

What good looks like: the evidence shows the observable the test plan names, for each behavior that plan does not defer. In `calib-01` the test plan is the configparser repro, expecting a clean parse, and the evidence shows `DuplicateOptionError` before and `parsed OK` after. "Tests pass", "works on my machine", or a run of the control path the repro says already succeeds, with the failing path absent, does not. A plan that names two failure modes needs both shown.

## Diff quality (harness category: unreviewable)

Used by `diff-reviewable`.

Where it lives:

- Eval: the fenced unified diff under `### Diff`, and the subjects under `### Commits`.
- Live: the output of `git diff main...HEAD`, and the commit subjects on that branch.

What good looks like: the hunks are the fix. In `calib-01` the diff deletes one shadowed line and leaves the effective value in place; nothing else is in the file. Debris is a debug print, a commented-out statement or earlier attempt, a function marked unused or dead, a TODO on code the plan does not change, or a hunk that only reformats or reprints lines the plan does not change. An explanatory comment beside the fix is not debris.

## Standards and comms (harness category: standards-wall)

Used by `template-honored`, `disclosure-present`, and `thread-aware`.

Where it lives:

- Eval: the pull-requests line and the contribution-policy line in `## Repo facts` (template sections, a required issue reference, a required changelog or whatsnew file, and any AI-disclosure rule). Read those against `### Description` and, for a required file, against `### Diff`. Maintainer direction is a member, owner, or maintainer comment in `## Thread highlights` that names a file, a forbidden API, a behavior to preserve, or an approach; read it against `### Description`.
- Live: the repo's PR template and `docs/CONTRIBUTING.md`, plus an AI-policy file if those point at one. Read them against the title and description in `pr_draft.md` and, for a required file, against `git diff main...HEAD`. Maintainer direction is the same kind of comment on the issue thread. A classmate's comment is not direction.

What good looks like: each required section contains a sentence about this change, a required `closes #` or `fixes #` uses this issue's number, and a required changelog or whatsnew file is in the diff unless the description says that item does not apply and why. In `calib-01` the repo-facts line says there is no PR template and no AI policy, and the description references `#2211`, so both the template check and the disclosure check pass. When a policy requires an AI disclosure, the description states the tool, the extent, or that the words are the author's own, whichever that policy asks for. When a maintainer comment names a constraint, the description follows it or says why this PR does not. Whether the description's "exactly the plan" claim matches the diff is plan fidelity, above.
