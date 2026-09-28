# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | Repo facts: "last 5 default-branch commits" (author and date). Live: the commit list on the repo front page. Measure dates against the bundle capture date, or against today in live mode. | At least one of those five commits is within 90 days and is either authored by a human (username does not end in `[bot]`) or is a bot commit that merged a human pull request. | required |
| repo-in-use | Repo facts: `archived:`, "latest release", and "last push to any branch". Live: the archive banner, the Releases box, and the newest commit date on the front page. | `archived` is false, and at least one of these is true: the latest release is within 365 days, or the last push is within 120 days. A missing release does not fail by itself. | required |
| unclaimed | Repo facts: "this issue: assignees:" and "linked PRs:". Also the Comments section for claim phrases and maintainer replies. | Assignees is empty, no linked PR is open, and the thread has no claim ("I'll take this", "working on this", "can I work on this", or the same idea) in the last 30 days that a maintainer has not declined. In live mode on Path Review, apply the house rule in `scope.md`: classmate claim comments do not fail this check. | required |
| ai-allowed | Repo facts: the "contribution policy" line (`CONTRIBUTING.md`, `AI_POLICY.md`, `AI_USAGE_POLICY.md`, and any AI checkbox in templates). | The policy does not ban AI-generated or AI-assisted contributions. Silence passes. Disclosure, testing, or "you must understand the change" conditions pass. | required |
| labeled-for-newcomers | The issue's labels. | The issue has at least one of `good first issue`, `good-first-issue`, `help wanted`, `beginner`, or `easy`. | preferred |
| repo-widely-used | Repo facts: the star count on the repo line. Live: the star count at the top of the repo page. | The repo has at least 500 stars. | preferred |
| issue-topic | The issue title and body. | The requested work is a software change: application code, tests, docs, tooling, or AI/ML behavior. Fail when the work is primarily hardware: circuits, PCB layout, physical fabrication, or device bring-up with no software change. | required |

## Verdict rule

Accept only if every required check is `pass`. A required `fail` or `unclear` rejects the issue. Preferred checks never change the verdict; use them only to rank issues that were accepted. `unclear` counts as `fail`.
