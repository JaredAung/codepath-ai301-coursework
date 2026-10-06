# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The plan's stated cause, read against the repro-evidence block: the observed behavior, the controls, and what those controls rule in or out. | The stated cause names a mechanism (a site, a missing check, a wrong value, or an ordering) that the repro evidence shows. Restating the symptom with no mechanism fails. A mechanism a control in that evidence rules out fails. No stated cause fails. | required |
| scope-bounded | The plan's stated change and any not-in-scope line, read against the change the issue and the repro evidence isolate. | The work is that one change, including the same defect at sites the issue or the repro already names. Extra work the issue did not ask for (a rewrite, a migration, a new option, a redesign, or unrelated areas) fails, even when the right fix is bundled inside it. Work the plan explicitly defers or marks not in scope does not fail the check. | required |
| executable | The plan's approach: the place it names and the change it says to make there, read against the files or areas the issue, the thread, or the repro already points at. | A stranger can start from the plan alone. It names a place and a concrete change there. "Profile and see", "poke around", "somewhere", or "whichever is easier", with no chosen place and no chosen change, fails. | required |
| test-decisive | The plan's test plan, read against the repro evidence's steps and the actual-versus-expected behavior those steps show. | The test names an observable result of exercising that behavior: the command, fixture, or scenario, and the outcome that would show the fix (an exit code, output, assertion, or a timing compared to a number the evidence states). "Run the suite", "should feel faster", or "nothing else breaks", with no outcome for this behavior, fails. No stated test fails. | required |
| unknowns-honest | Claims the plan treats as already decided, read against choices the same plan leaves open (unknown, unchecked, "not sure", or "whichever is easier"). | An open choice is labeled as unknown or deferred, and it is not also the decided cause or the decided fix. A plan that picks one option and defers the rest passes. A plan that never leaves a choice open passes. A plan that leaves the cause, the place, or the approach unpicked and still presents that as the plan to build fails. | required |
| thread-aware | The plan comment, read against maintainer direction in the thread highlights (eval) or the issue thread (live): a named file, cause, requested test, or approach from a maintainer, owner, or contributor. | If that direction is present, the comment follows it or says why this plan does not. If the thread has no such direction, the check passes. A comment that neither follows nor answers that direction fails. | required |
| disclosure-present | The plan comment, read against an AI-use disclosure rule in the repo-facts block (eval) or the repo's contribution docs (live). | If those sources require disclosing AI use, the plan comment includes that disclosure. If they require none, the check passes. A policy that only asks for a human in the loop, with no disclosure sentence, passes. | required |

## Verdict rule

Accept (ready to post and build from) only when every check in the table is `pass`. Reject (hold) when any check is `fail` or `unclear`. A `?` is written as `unclear`, and `unclear` counts as `fail`, so the package is held. Every check is `required`; none is `preferred`.
