# Scan, 2026-10-20

Four queries returned 400 unique issues. Ranking left 307. The top 5 were graded by fewest comments, at most 2 per repo. **1 accepted, 4 rejected.**

## Accepted

### 1. [selimfirat/pysad#373](https://github.com/selimfirat/pysad/issues/373)

Complete the type hints of `pysad.transform.probability_calibration`.

- **From:** query 1 (Python, `good first issue`). 0 comments, no assignee, updated within the last 24 hours.
- **Work:** add type hints, add the subpackage to the mypy override list in `pyproject.toml`, and make `pre-commit run --all-files` pass.
- **Fit:** Python, with a clear expected result and a check that can be run. No infrastructure, authentication, or migration work.
- **Stars:** `repo-min-stars` passes (302). `repo-widely-used` fails (under 500). Label: `good first issue`.
- **AI policy:** `AGENTS.md` says "We support the use of AI tools" and bans fully agent-generated contributions. The rubric passes. Review the change yourself and open the pull request as a draft.

## Rejected

| Issue | What sank it |
|---|---|
| [mloda-ai/mloda-registry#1154](https://github.com/mloda-ai/mloda-registry/issues/1154) | `repo-min-stars` fails (6 stars) |
| [eyadstein/leaklens#4](https://github.com/eyadstein/leaklens/issues/4) | `repo-min-stars` fails (0 stars). Repo created today. |
| [eyadstein/leaklens#3](https://github.com/eyadstein/leaklens/issues/3) | `repo-min-stars` fails (0 stars) |
| [CosturaAI/costura#18](https://github.com/CosturaAI/costura/issues/18) | `repo-min-stars` fails (2 stars). `unclaimed` is `unclear`: open PR #24 cross-references the issue, and its body was not read. |

`maintainer-alive`, `repo-in-use`, `ai-allowed`, and `issue-topic` passed for all five.

All five came from the `good first issue` queries (query 1 for four of them). Each had 0 comments, no assignee, a recent update, and the label, so comment count was the ordering signal.

Four of the five graded issues are brand-new, near-zero-star repos. Search results do not include a star count, so the 100-star floor only applies at grading. Query 2 (`good-first-issue`, Python) put nothing in the top 5.

```json
[
  {
    "item": "https://github.com/selimfirat/pysad/issues/373",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last 5 commits all within 1 day, by selimfirat (human)"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=false, latest release 2026-10-20, last push 2026-10-20"},
      {"name": "unclaimed", "grade": "pass", "evidence": "0 assignees, 0 comments, no cross-referenced PRs in timeline"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "AGENTS.md: 'We support the use of AI tools'; bans only fully agent-generated contributions"},
      {"name": "labeled-for-newcomers", "grade": "pass", "evidence": "Labelled good first issue"},
      {"name": "repo-min-stars", "grade": "pass", "evidence": "302 stars"},
      {"name": "repo-widely-used", "grade": "fail", "evidence": "302 stars, under 500"},
      {"name": "issue-topic", "grade": "pass", "evidence": "Add mypy type hints and an override entry; software change"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/mloda-ai/mloda-registry/issues/1154",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Commits by TKaltofen within 1 day"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=false, last push 2026-10-21"},
      {"name": "unclaimed", "grade": "pass", "evidence": "0 assignees, 0 comments"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No ban found in CONTRIBUTING.md; AGENTS.md is agent guidance"},
      {"name": "repo-min-stars", "grade": "fail", "evidence": "6 stars"},
      {"name": "issue-topic", "grade": "pass", "evidence": "Test constant refactor"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/eyadstein/leaklens/issues/4",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Commits by eyadstein within 1 day"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=false, last push 2026-10-21"},
      {"name": "unclaimed", "grade": "pass", "evidence": "0 assignees, 0 comments"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No policy files found; silence passes"},
      {"name": "repo-min-stars", "grade": "fail", "evidence": "0 stars, repo created 2026-10-20"},
      {"name": "issue-topic", "grade": "pass", "evidence": "Scanner feature in code"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/eyadstein/leaklens/issues/3",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Commits by eyadstein within 1 day"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=false, last push 2026-10-21"},
      {"name": "unclaimed", "grade": "pass", "evidence": "0 assignees, 0 comments"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No policy files found; silence passes"},
      {"name": "repo-min-stars", "grade": "fail", "evidence": "0 stars"},
      {"name": "issue-topic", "grade": "pass", "evidence": "Fuzzy duplicate check in leakage.py"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/CosturaAI/costura/issues/18",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Human commits by cauebraz within 1 day"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=false, last push 2026-10-20, no release (not failing)"},
      {"name": "unclaimed", "grade": "unclear", "evidence": "Timeline shows open PR #24 cross-referencing the issue; body not read"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No ban found in CONTRIBUTING.md or AGENTS.md"},
      {"name": "repo-min-stars", "grade": "fail", "evidence": "2 stars"},
      {"name": "issue-topic", "grade": "pass", "evidence": "Add tests to api.test.ts"}
    ],
    "verdict": "reject"
  }
]
```

# Direct grades

Hand-fed URLs. **2 accepted.** Both pass every required check and both preferred checks. Neither is Python or React.

## Accepted

### 1. [OpenChemistry/avogadrolibs#3191](https://github.com/OpenChemistry/avogadrolibs/issues/3191)

Remove forced layout direction from `.ui` files so right-to-left locales mirror correctly.

| Check | Grade | Evidence |
|---|---|---|
| maintainer-alive | pass | Latest commits by ghutchis on 2026-10-20 |
| repo-in-use | pass | Not archived. Release 2.0.0 on 2026-04-01. Pushed 2026-10-20 |
| unclaimed | pass | No assignees, 0 comments, no open PR referencing #3191 |
| ai-allowed | pass | `CONTRIBUTING.md`: levels 0 and 1 are probably fine. Level 1 is full human review. Level 2, pair programming with the model, is outside the policy. The project may reject mostly ML-generated work. Human-reviewed, human-implemented help passes. |
| repo-min-stars | pass | 690 stars |
| issue-topic | pass | Qt `.ui` change: remove `layoutDirection` from 2 files |
| labeled-for-newcomers | pass | `good first issue`, `help wanted` |
| repo-widely-used | pass | 690 stars |

**Fit:** 4 occurrences in 2 files, with exact steps. C++/Qt, and there is no test. Verification is running the dialogs with `-reverse` and attaching screenshots.

### 2. [code-charity/youtube#4407](https://github.com/code-charity/youtube/issues/4407)

SPA race condition: subtitles and auto-dubbing fail to apply.

| Check | Grade | Evidence |
|---|---|---|
| maintainer-alive | pass | Newest commit 2026-10-11. ImprovedTube2 is merging human PRs |
| repo-in-use | pass | Not archived. Release v4.2027 on 2026-05-30. Pushed 2026-10-11 |
| unclaimed | pass | No assignees, no comments, no PR that references the issue |
| ai-allowed | pass | No `CONTRIBUTING.md`, `AI_POLICY.md`, or `AGENTS.md`. Silence passes. Issue templates were not checked |
| repo-min-stars | pass | 4642 stars |
| issue-topic | pass | JavaScript change in `player.js` |
| labeled-for-newcomers | pass | `good first issue`, `help wanted`, `up-for-grabs` |
| repo-widely-used | pass | 4642 stars |

**Fit:** a browser extension in JavaScript. The proposed fix is a retry helper with exponential backoff. Behavior depends on the player, and there is no obvious test location. It also has the `Feature request` label, so the scope is looser than avogadrolibs#3191.

```json
[
  {
    "item": "https://github.com/OpenChemistry/avogadrolibs/issues/3191",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Latest commits by ghutchis on 2026-10-20"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; release 2.0.0 on 2026-04-01; pushed 2026-10-20"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignees, 0 comments, no open PR referencing #3191"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md: \"levels 0 and 1 are probably fine\"; human-implemented, fully reviewed AI help allowed; no outright ban"},
      {"name": "labeled-for-newcomers", "grade": "pass", "evidence": "Labels: good first issue, help wanted"},
      {"name": "repo-min-stars", "grade": "pass", "evidence": "690 stars"},
      {"name": "repo-widely-used", "grade": "pass", "evidence": "690 stars >= 500"},
      {"name": "issue-topic", "grade": "pass", "evidence": "Remove layoutDirection from 2 .ui files; a Qt code change"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/code-charity/youtube/issues/4407",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "ImprovedTube2 merging human PRs on 2026-10-11"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; release v4.2027 on 2026-05-30; pushed 2026-10-11"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignees, 0 comments, no open PR referencing #4407"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "No CONTRIBUTING.md, AI_POLICY.md or AGENTS.md found; silence passes"},
      {"name": "labeled-for-newcomers", "grade": "pass", "evidence": "Labels: good first issue, help wanted, up-for-grabs"},
      {"name": "repo-min-stars", "grade": "pass", "evidence": "4642 stars"},
      {"name": "repo-widely-used", "grade": "pass", "evidence": "4642 stars >= 500"},
      {"name": "issue-topic", "grade": "pass", "evidence": "JavaScript retry helper for player.js"}
    ],
    "verdict": "accept"
  }
]
```
