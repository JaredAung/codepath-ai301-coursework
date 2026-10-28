# Contribution: [GOOD FIRST ISSUE] Add VectorStoreFactorySpec: backend names, file-backed SQLite and Qdrant factory paths

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Jared Aung
**GitHub Username:** JaredAung
**Issue:** https://github.com/llm4s/llm4s/issues/2225
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout and a Python and React search strategy, then patched the rubric after the first scan.**

I built issue-scout from the Unit 1 skill and wrote four `gh search issues` queries from the fit profile, Python and TypeScript with React under both `good first issue` and `good-first-issue`, with filters that drop assigned issues, keep the last 90 days, and order by fewest comments, at most two issues per repo. On 2026-10-20 the scan graded five issues and accepted only selimfirat/pysad#373. Four of those five were under 100 stars, because search results do not include a star count, and an earlier newest-update tie-break had filled a shortlist with issues opened the same hour. I split stars into a required 100-star check and a preferred 500-star check, dropped that tie-break, taught `ai-allowed` to read `AGENTS.md`, and made `unclaimed` fail only when a pull request references that issue.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

The 2026-10-20 scan did not surface this issue. Four queries built a top 5, and the scout accepted only selimfirat/pysad#373. The other four failed `repo-min-stars`. I graded [llm4s/llm4s#2225](https://github.com/llm4s/llm4s/issues/2225) later, in direct mode, on 2026-10-27. The verdict was `accept`. Every required check passed, including `scope-feasible`: one new spec, `VectorStoreFactorySpec.scala`, with the cases listed. `repo-widely-used` failed at 277 stars and did not change the verdict. The difficulty note was straightforward. The issue names the file, the spec to copy (`VectorStoreSpec.scala`), and the cases, and the tests run offline.

It is Scala, not the Python or React work in my fit profile. I took it because the expected behavior is written down and the work is a test I can make fail on purpose. I want to learn how to read a factory I have not seen, confirm the uncovered branches, and keep the spec inside the issue: `Backend.fromString`, file-backed SQLite, the offline Qdrant paths, `KeywordIndex.sqlite`, and `HybridSearcher.sqlite`, with pgvector left out. The scan still cannot see stars until grading, so most of a shortlist can be rejects. That part did not hold up. The direct grade did: it found no assignee and no comments, it did not let fit overturn the verdict, and the difficulty note told me the edge was small. Claim comment: https://github.com/llm4s/llm4s/issues/2225#issuecomment-6460109390

**Toolkit**

- Tool: issue-scout, direct mode on llm4s/llm4s#2225, after the 2026-10-20 scan
- What it produced: verdict `accept`, difficulty straightforward. `scope-feasible` passed. `repo-widely-used` failed at 277 stars and did not change the verdict.
- Difficulties: the scan never returned this issue, and `gh search issues` still has no star count, so four of the five issues graded on 2026-10-20 failed `repo-min-stars`. Fit is Python and React. The rubric accepted a Scala test issue because fit cannot change a verdict. `ai-allowed` passed on silence in `CONTRIBUTING.md`. The read-out stayed in the session until it was copied into `scan-output.md`.
- What changed: the scope patch. Unit 1 had no row for whether an issue is one piece of work, so nothing rejected an umbrella issue and nothing recorded an open edge. I added required check `scope-feasible`, which fails only when there is no single piece of work, and a difficulty note under the checks table. The note does not change accept or reject. On this issue it came back straightforward.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
