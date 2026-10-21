# Scan notes, 2026-10-20

One accept: [selimfirat/pysad#373](https://github.com/selimfirat/pysad/issues/373). Four rejects, all sunk by `repo-min-stars`: mloda-registry#1154 (6), leaklens#4 (0), leaklens#3 (0), costura#18 (2).

## Patches already in the rubric

- Stars are split. `repo-min-stars` requires 100. `repo-widely-used` prefers 500 and does not change the verdict. This scan is the first run with that split. It did the job: the 0-star and 6-star repos were rejected. PySAD at 302 passes the minimum and fails the preferred check, so it stays accepted and ranks below a 500-star repo.
- `ai-allowed` now reads `AGENTS.md` and any contributing doc `CONTRIBUTING.md` links to. This run quoted `AGENTS.md` instead of a file that is not there. The pass still feels tight. PySAD says "We support the use of AI tools" and also "Fully agent-generated contributions are banned." The rubric is right to pass that. If I take #373, I review the change myself and open the pull request as a draft.
- `unclaimed` fails only when a pull request references that issue. costura#18 was still graded `unclear` because this run did not read PR #24's body. That body says "Closes #18". The check is already specific enough. `unclear` counts as fail, and `repo-min-stars` had already rejected the issue.

## Still open

- Ranking cannot see stars. `gh search issues` does not return a star count, so `repo-min-stars` only runs at grading. Four of the five graded slots were rejects under 100 stars. A star floor in `search-strategy.md` needs another search, such as `gh search repos`, or I accept the wasted grades.
- Query 2 (`good-first-issue`, Python) put nothing in the top 5. It may duplicate query 1. Leave it for one more scan before deleting it.
- Fewest-comments-first still surfaces empty, just-opened issues, including a repo created today. The newest-update tie-break is already gone. If the next shortlist looks like this one, the order rule needs another pass.
