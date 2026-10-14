# Procedure: how this tool grades a PR package

## Read order

Read in this order before grading any check. The plan is read before the diff so the boundary is written down before the diff can look reasonable on its own. The description is read after the diff so a fidelity claim is compared to hunks already noted. The test evidence is read last, against the test plan already noted.

1. In live mode, read `scope.md` before the package. If the `Repo:` line is empty or still a placeholder, stop and tell the student to fill it with their section's Path Review repo. If the issue is not in that repo, refuse to grade. Write down the house rules that change a read: a classmate's comment is not maintainer direction, and one PR delivers the posted plan for one issue. In eval mode, do not read `scope.md`.
2. In both modes, read `rubric.md`. If the checks table has no filled row, or this file has no numbered steps, stop and say the tool cannot grade. Write down every check name, its evidence sentence, its pass condition, and its weight, in table order. Write down the verdict rule, including that `unclear` counts as `fail`.
3. Read `references/evidence-guide.md`. For each check, note which heading locates that evidence.
4. Read the whole package before grading any check. From each part, write only the notes named here:
   1. Issue. Eval: the Issue section. Live: the issue page. Note the issue number and the behavior it asks to change.
   2. Thread. Eval: Thread highlights. Live: the issue's comment thread. Note any direction from a member, owner, or maintainer: a named file, a forbidden API, a behavior to preserve, or an approach. If there is none, write `no maintainer direction`. A classmate's comment, in live mode, is not direction.
   3. Repo asks. Eval: the Repo facts block, the pull-requests line and the contribution-policy line. Live: the PR template and `docs/CONTRIBUTING.md`, plus an AI-policy file if those point at one. Note each required section, issue-reference form, and required file. Note whether an AI disclosure is required and the sentence it requires. If none is required, write `no disclosure required`. Note a named test command if one is stated.
   4. Plan, before the diff. Eval: the Plan context section. Live: `plan.md` only. Note the in-scope change, the files or areas it names, every not-in-scope line, every deviation or deferral note, and the test plan's behaviors (the command or scenario and the outcome). If a behavior is only in a deferral note, mark it deferred.
   5. Diff, after the plan. Eval: the Diff and Commits sections. Live: the output of `git diff main...HEAD` run from the working copy. Note each changed file, what each hunk changes, and any debris: a debug print, commented-out statement, dead or unused function, TODO on unchanged code, or a hunk that only reformats lines the plan does not change.
   6. Draft text, after the diff. Eval: Title and Description. Live: `pr_draft.md`. Note what the description says changed, any "exactly the plan" or "no other changes" claim, any deliverable it says is done, and whether it restates a deviation note. Note whether each repo ask from step 4.3 is filled, and whether the disclosure from step 4.3 is present.
   7. Test evidence, last. Eval: the Test evidence section. Live: `test_evidence.md`. Note the scenario and the outcome shown for each behavior from step 4.4. If the section is missing or says none provided, write `no test evidence`.

## Evidence gathering

Gather from the notes in Read order. Do not open other files. In eval mode, quote the bundle line. In live mode, quote the file or command named in the step.

1. Plan fidelity, for `plan-fidelity`. Record the plan's in-scope change, its not-in-scope lines, and any deviation note. Next to that, record each diff file and the behavior each hunk changes. Then record the description's claim about what changed. Sources: Read order steps 4.4, 4.5, and 4.6.
2. Test evidence, for `test-decisive`. Record each behavior the test plan names, and whether step 4.4 marked it deferred. Next to each one that is not deferred, record the scenario and outcome from step 4.7, or `not shown`. If step 4.3 names a test command, record whether step 4.7 shows that command's outcome. Source: Read order steps 4.3, 4.4, and 4.7.
3. Diff quality, for `diff-reviewable`. Record any debris noted in step 4.5. If there is none, write `no debris`. Source: Read order step 4.5.
4. Standards, for `template-honored`. Record each required section, issue reference, and required file from step 4.3, and whether step 4.6 or the diff meets it. If the source says there is no PR template, write `no PR template` and record only the remaining issue-reference or test-file ask. Source: Read order steps 4.3, 4.5, and 4.6.
5. Standards, for `disclosure-present`. Record the disclosure rule from step 4.3, or `no disclosure required`. Record whether the description includes it. Source: Read order steps 4.3 and 4.6.
6. Standards, for `thread-aware`. Record the direction from step 4.2, or `no maintainer direction`. Record whether the description follows it or says why it does not. Source: Read order steps 4.2 and 4.6.

## Check execution

1. Grade from the gathered notes only. Do not re-read the package. Re-read one section only if the gathering step for that section was skipped and its note is blank. A note that says `no maintainer direction`, `no disclosure required`, `no PR template`, `no test evidence`, `no debris`, or `not shown` is a finished note, not a skipped step.
2. Grade in this order: `plan-fidelity`, `test-decisive`, `diff-reviewable`, `template-honored`, `disclosure-present`, `thread-aware`.
3. For each check, apply that row's pass condition to its gathered note and to nothing else. Grade `pass` or `fail`. Set `evidence` to the one fact or quote that decided the grade.
4. Apply absence this way, and no other way:
   - `plan-fidelity`: no plan, or a diff with no notes, is `fail`.
   - `test-decisive`: `no test evidence`, or a named behavior `not shown`, is `fail`. A deferred behavior that is `not shown` is not a fail.
   - `diff-reviewable`: `no debris` is `pass`.
   - `template-honored`: `no PR template`, with any remaining issue-reference or test-file ask met, is `pass`. A required section or file with no content is `fail`.
   - `disclosure-present`: `no disclosure required` is `pass`. A required disclosure that is absent is `fail`.
   - `thread-aware`: `no maintainer direction` is `pass`.
5. Grade `unclear` only when the section that check reads is missing from the package, so the note could not be taken. Set `evidence` to `absent: <section name>`. Do not use `unclear` for a section you did not open, and do not use it when step 4 already says that absence is `pass` or `fail`.
6. If the pass condition says `pass` and the grade feels wrong, the grade stays `pass`. Write the tension in the summary. Do not invent a check that is not in the table.

## Verdict assembly

1. Apply the verdict rule in `rubric.md`. Verdict is `accept` only when every check is `pass`. Verdict is `reject` when any check is `fail` or `unclear`.
2. `unclear` counts as `fail`. There is no third verdict. No check in the table is `preferred`.
3. The deciding check is the first check in the grade order that is `fail` or `unclear`. In the summary, quote that check's name and its one-line `evidence`. If the verdict is `accept`, the summary says every check passed and quotes the `plan-fidelity` evidence line.
4. In live mode, read `voice-guide.md` and compare the draft title and description to each rule. In the summary, quote any rule the draft breaks. The voice guide does not change the verdict. In eval mode, do not read `voice-guide.md`.
5. Emit a short summary (one line per check, the deciding-check quote, and any voice-guide notes), then a fenced JSON block, then nothing after it. `item` is the pull request URL in live mode, or the bundle id in eval mode. `checks` lists every check in grade order with `name`, `grade`, and `evidence`. `verdict` is `accept` or `reject`.
