# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives:

- Eval: the cause sentence in `## Candidate plan`. It may be under a heading such as Diagnosis, Cause, or Problem statement, or it may be an unlabeled paragraph that names why the behavior happens. Read it against `## Repro evidence` (Steps, any control run, Expected, and Actual) and against the behavior in `## Issue`. When the plan says it is following a comment, also read that comment in `## Thread highlights`.
- Live: the cause sentence in the draft `plan.md`, read against the student's posted repro comment on the issue. On the house issue, the reproduction evidence is the house repro pack as quoted in the drafts. If the drafts quote no repro evidence, record that absence. Read the issue body, and any comment the plan says it follows, from the issue thread.

What good looks like: the stated cause names a mechanism that produces the behavior in the repro's Actual, including what the control run shows. In `calib-01`, the cause is that the branch-commits view keeps its pre-push flags, and the Actual says the color updates only after leaving and re-entering that view. A cause that the repro's control rules out, or that explains a different behavior than the one the steps produced, does not follow from the evidence. A thread comment is grounding only when the repro shows the claim that comment makes.

## Scope

Where it lives:

- Eval: the bound in `## Candidate plan`: the in-scope line, the not-in-scope or deferred line, and the files or areas named beside them. Headings vary (Scope, Proposed changes, or sentences that say "In:" and "Out:"). Read that bound against the behavior `## Issue` and `## Repro evidence` actually cover.
- Live: those same lines in the draft `plan.md`, read against the issue body and the posted repro comment.

What good looks like: the plan names one change that would alter the reproduced behavior, and it names what it will leave alone. In `calib-01`, in-scope is the push-completion callback adding the commits context to the post-push refresh, and out-of-scope is how push status is computed and how other views refresh. A plan that also rewrites, migrates, or adds behavior the issue and the repro do not require is more than one change. A plan that says it will look around until it finds the bug names no bound.

## Executability

Where it lives:

- Eval: the work statements in `## Candidate plan`: a file or area, the change to make there, and the order of the steps. These may sit under Files, Approach, Proposed changes, or Changes, or in the same paragraph as the cause. Read them against the cause and the bound already gathered.
- Live: those same statements in the draft `plan.md`.

What good looks like: someone who has not talked to the author can start. The plan names a file or area, the change to make there, and which step comes first. In `calib-01`, the first action is in `pkg/gui/controllers/sync_controller.go`: the push completion callback adds the commits context to its post-push refresh scope. A plan whose next step is "poke around the editor code" or "send a PR" cannot be started from the text alone.

## Test plan

Where it lives:

- Eval: the success check in `## Candidate plan` (Test plan, Test, or the sentences that say how the author will know it worked), read against the triggering step and the observable in `## Repro evidence` (the output text, exit code, timing, or on-screen result in Actual, and the control).
- Live: that success check in the draft `plan.md`, read against the steps and the observed result in the posted repro comment.

What good looks like: the check re-runs the repro's triggering step and names the same observable the Actual recorded. In `calib-01`, the test is the repro steps, and at step 3 the color must flip without leaving the view. A check that only says the suite passes, or that the bug is fixed, names nothing the repro showed.

## Honesty

Where it lives:

- Eval: risk, unknown, assumption, and deviation sentences in `## Candidate plan`, read against every cause, file, and outcome that same plan states as fact.
- Live: those sentences in the draft `plan.md`. After a build, a deviation lives in the plan's deviations note: what changed and why. A change that appears only in the diff is absent from the package.

What good looks like: a claim the plan has not checked is labeled unknown, unverified, or a risk, and the cause it will build still matches the repro. A stated risk that names what is unmeasured, and what the plan will do if that measurement goes the wrong way, is an honest unknown. A file, a root cause, or a ship date stated as fact, in a plan that also says the author has not looked, is false confidence.

## Comms

Where it lives:

- Eval: `## Candidate plan comment`, read against `## Thread highlights` and against the contribution policy in `## Repo facts` (including any AI-use or disclosure rule, and any contributing ask). The bug-report template line in that block is a reporter ask; use it only when the policy says comments must follow it.
- Live: the draft plan comment, read against maintainer and owner comments on the issue thread and against the repo's contributing docs and AI policy. Also read `scope.md` for the Path Review house rules. A classmate's existing plan comment is not a block, and "same approach as above" is not this package's plan.

What good looks like: the comment names this issue's reproduced behavior and the change the plan will make, and it answers a direction or constraint a thread comment actually states. In `calib-01`, the comment names the missed refresh in the branch-commits context and the review-bandwidth note from CONTRIBUTING, on a thread with no comments. If the repo-facts contribution policy requires an AI-use disclosure, the comment includes the disclosure that policy asks for. If the policy states no AI disclosure requirement, or no AI policy, the comment needs none. A comment that could be pasted onto a different issue, or that skips a maintainer direction the thread states, does not meet this.
