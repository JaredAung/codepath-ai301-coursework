# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Used by `environment-recorded` and `commit-pinned`.

Where it lives:

- Eval: the environment record in the candidate repro report. Read the runtime, version, and platform against the issue context. Read any commit, tag, or release against the issue context and the repo-facts block.
- Live: the environment record in the draft repro comment. Read the runtime, version, and platform against the issue body. Read any commit, tag, or release against the issue body and the repo's docs.

What good looks like: the record names the runtime, its version, and the operating system. If any of those differs from what the issue states, the report says so. When the issue or the repo-facts block names a commit, tag, or release, the report names the one it ran against. A record that omits the runtime or version the issue's behavior depends on is not sufficient. If neither source names a commit, tag, or release, the pin is not required.

## Steps

Used by `steps-followable`.

Where it lives:

- Eval: the reproduction steps in the candidate repro report, from the stated starting state through the action that triggers the behavior.
- Live: those same steps in the draft repro comment.

What good looks like: someone with the recorded environment can reach the trigger using only the commands, files, and inputs written in the steps. A step that needs a command, file, or input the report never states is not followable.

## Behavior shown

Used by `behavior-matches`.

Where it lives:

- Eval: the output excerpt, log, or screenshot in the candidate repro report, read against the behavior or error described in the issue context.
- Live: that same artifact in the draft repro comment, read against the behavior or error in the issue body.

What good looks like: the artifact shows the behavior the issue describes, or it shows that behavior is absent and the report says cannot-reproduce. An artifact that shows a different error, a setup failure, or a different bug does not show this issue.

## Honesty

Used by `outcome-honest`.

Where it lives:

- Eval: the outcome sentence in the candidate repro report (reproduced, cannot reproduce, or partial), read against the output excerpt, log, or screenshot in that same report.
- Live: that outcome sentence in the draft repro comment, read against the artifact in the same comment.

What good looks like: the stated outcome is what the artifact supports. An evidenced cannot-reproduce meets this. A reproduction claim whose artifact shows something else, or any claim the artifact does not support, does not.

## Comms

Used by `claim-specific` and `disclosure-present`.

Where it lives:

- Eval: the candidate claim comment, read against the issue title and body in the issue context. Each candidate comment, read against an AI-use or other disclosure rule in the repo-facts block.
- Live: the draft claim comment, read against the issue title and body. Each draft comment, read against an AI-use or other disclosure rule in the repo's contribution docs.

What good looks like: the claim names the behavior in this issue, or the specific part of it being reproduced. A claim that could be pasted onto a different issue does not. If the repo-facts block or the contribution docs require a disclosure, each comment being graded includes it. If they require none, the disclosure check passes.
