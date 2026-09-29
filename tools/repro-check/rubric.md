# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The environment record in the repro report, read against the runtime, version, and platform named in the issue. | The record names the runtime, its version, and the operating system. If any of those differs from what the issue states, the report says so. A record that omits the runtime or version the issue's behavior depends on fails. | required |
| steps-followable | The reproduction steps in the repro report, from the stated starting state through the action that triggers the behavior. | Someone with the recorded environment can reach the trigger using only the commands, files, and inputs written in the steps. A missing command, file, or input fails the check. | required |
| behavior-matches | The output excerpt, log, or screenshot in the repro report, read against the behavior or error the issue describes. | The artifact shows that behavior, or it shows the behavior is absent and the report says cannot-reproduce. A different error, a setup failure, or a different bug fails. | required |
| outcome-honest | The report's stated outcome (reproduced, cannot reproduce, or partial), read against the artifacts in the same report. | The stated outcome is what the artifacts support. An evidenced cannot-reproduce passes. A reproduction claim whose artifact shows something else, or any claim the artifact does not support, fails. | required |
| claim-specific | The claim comment, read against the issue title and body. | The comment names the behavior in this issue, or the specific part of it being reproduced. A comment that could be pasted on a different issue fails. | required |
| disclosure-present | Each draft comment, read against an AI-use or other disclosure rule in the repo-facts block (eval) or the repo's contribution docs (live). | If those sources require a disclosure, each comment being graded includes it. If they require none, the check passes. | required |
| commit-pinned | The environment record or the steps, read against a commit, tag, or release named in the issue or the repo-facts block. | The report names the commit, tag, or release it ran against when one of those sources identifies one. If neither source identifies one, the check passes. | preferred |

## Verdict rule

Accept only when every required check is `pass`. A required `fail` or `unclear` is reject. Preferred checks are reported and never change the verdict. On a claim-only draft, leave `environment-recorded`, `steps-followable`, `behavior-matches`, `outcome-honest`, and `commit-pinned` out of the rule; apply the same rule to `claim-specific` and `disclosure-present` only.
