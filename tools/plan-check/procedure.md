# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. In live mode, read `scope.md` before the package. If the `Repo:` line is still a placeholder, stop and tell the student to get the cohort scope file. If the issue is not in that repo, refuse to grade. Write down the house rules that change how evidence is read: another student's plan comment does not block this package, and a comment that only says "same approach as above" is not a plan. In eval mode, do not read `scope.md`.
2. In both modes, read `rubric.md`. Write down every check name, its evidence sentence, its pass condition, and its weight, in table order. Write down the verdict rule, including that a `?` is `unclear` and that `unclear` counts as `fail`.
3. Read `references/evidence-guide.md`. For each check, note which heading locates that evidence. If a heading is still the template comment, use the package locations in Evidence gathering below.
4. Read the whole package before grading any check. Read the repro evidence before the plan so the behavior is noted before the plan's cause is seen. From each part, write only the notes named here:
   1. Issue context. Eval: the Issue section. Live: the issue page. Note the change the issue asks for and the expected behavior.
   2. Thread. Eval: Thread highlights. Live: the issue's comment thread. Note any direction from a maintainer, owner, or contributor: a named file, cause, requested test, or approach. If there is none, write `no maintainer direction`.
   3. Repo conventions. Eval: the Repo facts block. Live: `CONTRIBUTING.md`, `AI_POLICY.md`, and the issue templates, via `gh` or the web. Note whether those sources require an AI-use disclosure and the sentence they require. If they do not, write `no disclosure required`.
   4. Repro evidence. Eval: the Repro evidence section. Live: the student's posted repro comment. On the house issue, use the house repro pack only as the drafts quote it. Note the observed behavior, each control, what that control rules in or out, and the actual versus expected outcome. If the drafts quote no repro evidence, write `no repro evidence`.
   5. Candidate plan. Eval: the Candidate plan section. Live: `plan.md` only, not other files in the working directory. Note the stated cause, the stated change, any not-in-scope or deferred line, the place and the change to make there, the test, and any choice left open (`unknown`, `unchecked`, `not sure`, or `whichever is easier`).
   6. Candidate plan comment. Eval: the Candidate plan comment section. Live: the draft plan comment only. Note whether it follows the direction from step 4.2 or says why it does not, and whether it includes the disclosure from step 4.3.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

Gather from the notes in Read order. Do not open other files. In eval mode, quote the bundle line. In live mode, the issue page, thread, and repo docs are the issue side; `plan.md` and the draft plan comment are the candidate side.

1. Diagnosis and grounding, for `diagnosis-grounded`. Record the plan's stated cause in one sentence. Next to it, record the repro behavior and what each control rules out. Sources: Read order steps 4.4 and 4.5. If step 4.4 is `no repro evidence` or step 4.5 has no cause, record that phrase.
2. Scope, for `scope-bounded`. Record the plan's stated change, every not-in-scope or deferred line, and the one change the issue and the repro isolate. Sources: Read order steps 4.1, 4.4, and 4.5.
3. Executability, for `executable`. Record the place the plan names and the change it says to make there. If it names no place, record `no place`. If it names no change, record `no change`. Source: Read order step 4.5, compared with places already named in steps 4.1, 4.2, or 4.4.
4. Test plan, for `test-decisive`. Record the plan's test: the command, fixture, or scenario, and the outcome it names. Next to it, record the repro steps and the actual-versus-expected outcome. If the plan names no test, record `no test`. Sources: Read order steps 4.4 and 4.5.
5. Honesty, for `unknowns-honest`. Record each choice the plan leaves open, and record whether that same plan also states a decided cause and a decided fix. Source: Read order step 4.5 only.
6. Comms, for `thread-aware`. Record the maintainer direction from Read order step 4.2, or `no maintainer direction`. Record whether the plan comment follows that direction or says why it does not. Source: Read order steps 4.2 and 4.6.
7. Comms, for `disclosure-present`. Record the disclosure rule from Read order step 4.3, or `no disclosure required`. Record whether the plan comment includes that disclosure. Source: Read order steps 4.3 and 4.6.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Grade from the gathered notes only. Do not re-read the package. Re-read one section only if the gathering step for that section was skipped and its note is blank. A note that says `no repro evidence`, `no place`, `no change`, `no test`, `no maintainer direction`, or `no disclosure required` is a finished note, not a skipped step.
2. Grade in this order: `diagnosis-grounded`, `scope-bounded`, `executable`, `test-decisive`, `unknowns-honest`, `thread-aware`, `disclosure-present`.
3. For each check, apply that row's pass condition to its gathered note and to nothing else. Grade `pass` or `fail`. Set `evidence` to the one fact or quote that decided the grade. "Looks fine" is not evidence.
4. Apply absence this way, and no other way:
   - `diagnosis-grounded`: `no repro evidence` or no stated cause is `fail`.
   - `executable`: `no place` or `no change` is `fail`.
   - `test-decisive`: `no test` is `fail`.
   - `thread-aware`: `no maintainer direction` is `pass`.
   - `disclosure-present`: `no disclosure required` is `pass`.
   - `scope-bounded` and `unknowns-honest`: grade from the note with the row's pass condition. Do not treat a missing not-in-scope line as a fail by itself.
5. Grade `unclear` only when the section that check reads is missing from the package, so the note could not be taken. Set `evidence` to `absent: <section name>`. Do not use `unclear` for a section you did not open, and do not use it when step 4 already says that absence is `pass` or `fail`.
6. If the pass condition says `pass` and the grade feels wrong, the grade stays `pass`. Write the tension in the summary. Do not invent a check that is not in the table.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Apply the verdict rule in `rubric.md`. Verdict is `accept` only when every check is `pass`. Verdict is `reject` when any check is `fail` or `unclear`.
2. Write a `?` as `unclear`. `unclear` counts as `fail`, so the verdict is `reject`. There is no third verdict. No check is `preferred`.
3. The deciding check is the first check in the grade order that is `fail` or `unclear`. In the summary, quote that check's name and its one-line `evidence`. If the verdict is `accept`, the summary says every check passed and quotes the `diagnosis-grounded` evidence line.
4. In live mode, read `voice-guide.md` and compare the draft plan comment to each rule. In the summary, quote any rule the draft breaks. The voice guide does not change the verdict. In eval mode, do not read `voice-guide.md`.
5. Emit a short summary (one line per check, the deciding-check quote, and any voice-guide notes), then a fenced JSON block, then nothing after it. `item` is the issue URL in live mode or the bundle id in eval mode. `checks` lists every check in grade order with `name`, `grade`, and `evidence`. `verdict` is `accept` or `reject`.
