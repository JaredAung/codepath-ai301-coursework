# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/9

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]



**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Here's the grading, per the rubric in rubric.md.

Repo-level facts (apply to all three): not archived, last push 2026‑09‑16 (11 days before today, within 120d), no releases published, 3 stars, last 5 commits all by a human (Aburke225) within 90 days, CONTRIBUTING.md has no AI restriction and no AI_POLICY.md/AGENTS.md exists — silence passes. Only 5 PRs exist in the whole repo and none close #28, #16, or #9.

#28 — Add rate limiting per IP address

┌───────────────────────┬───────┬───────────────────────────────────────────────┐
│         Check         │ Grade │                   Evidence                    │
├───────────────────────┼───────┼───────────────────────────────────────────────┤
│ maintainer-alive      │ pass  │ last commit 2026-09-16, human author          │
├───────────────────────┼───────┼───────────────────────────────────────────────┤
│ repo-in-use           │ pass  │ not archived, pushed 11 days ago              │
├───────────────────────┼───────┼───────────────────────────────────────────────┤
│ unclaimed             │ pass  │ assignees: [], comments: [], no PR closes #28 │
├───────────────────────┼───────┼───────────────────────────────────────────────┤
│ ai-allowed            │ pass  │ no ban in CONTRIBUTING.md                     │
├───────────────────────┼───────┼───────────────────────────────────────────────┤
│ labeled-for-newcomers │ fail  │ labels: enhancement, safety, tier-2           │
├───────────────────────┼───────┼───────────────────────────────────────────────┤
│ repo-widely-used      │ fail  │ 3 stars                                       │
├───────────────────────┼───────┼───────────────────────────────────────────────┤
│ issue-topic           │ pass  │ FastAPI middleware addition — software change │
└───────────────────────┴───────┴───────────────────────────────────────────────┘

Verdict: accept

#16 — Failed tool calls never reach review output

┌───────────────────────┬───────┬─────────────────────────────────────────────────┐
│         Check         │ Grade │                    Evidence                     │
├───────────────────────┼───────┼─────────────────────────────────────────────────┤
│ maintainer-alive      │ pass  │ same repo facts                                 │
├───────────────────────┼───────┼─────────────────────────────────────────────────┤
│ repo-in-use           │ pass  │ same repo facts                                 │
├───────────────────────┼───────┼─────────────────────────────────────────────────┤
│ unclaimed             │ pass  │ assignees: [], comments: [], no PR closes #16   │
├───────────────────────┼───────┼─────────────────────────────────────────────────┤
│ ai-allowed            │ pass  │ no ban                                          │
├───────────────────────┼───────┼─────────────────────────────────────────────────┤
│ labeled-for-newcomers │ fail  │ labels: bug, agent, tier-2                      │
├───────────────────────┼───────┼─────────────────────────────────────────────────┤
│ repo-widely-used      │ fail  │ 3 stars                                         │
├───────────────────────┼───────┼─────────────────────────────────────────────────┤
│ issue-topic           │ pass  │ surface failures from orchestrator to review    │
│                       │       │ service — software change                       │
└───────────────────────┴───────┴─────────────────────────────────────────────────┘

Verdict: accept

#9 — Caching layer for repeated portfolio queries

┌───────────────────────┬───────┬──────────────────────────────────────────────┐
│         Check         │ Grade │                   Evidence                   │
├───────────────────────┼───────┼──────────────────────────────────────────────┤
│ maintainer-alive      │ pass  │ same repo facts                              │
├───────────────────────┼───────┼──────────────────────────────────────────────┤
│ repo-in-use           │ pass  │ same repo facts                              │
├───────────────────────┼───────┼──────────────────────────────────────────────┤
│ unclaimed             │ pass  │ assignees: [], comments: [], no PR closes #9 │
├───────────────────────┼───────┼──────────────────────────────────────────────┤
│ ai-allowed            │ pass  │ no ban                                       │
├───────────────────────┼───────┼──────────────────────────────────────────────┤
│ labeled-for-newcomers │ fail  │ labels: enhancement, devops, rag, tier-2     │
├───────────────────────┼───────┼──────────────────────────────────────────────┤
│ repo-widely-used      │ fail  │ 3 stars                                      │
├───────────────────────┼───────┼──────────────────────────────────────────────┤
│ issue-topic           │ pass  │ content-hash cache — software change         │
└───────────────────────┴───────┴──────────────────────────────────────────────┘

Verdict: accept

All three clear every required check — same rejects on both preferred checks too (no newcomer label, same star count), so nothing in the rubric's preferred checks separates them. scope.md's fit-profile section is still the placeholder text (Write a few sentences here.), so I have no real signal to rank on — filling that in (languages/tools you've used, what you want to practice, what to avoid) would let a future run actually order these. One objective (non-fit) note if it helps: #9 touches two files for a self-contained cache, while #28 and #16 both require wiring across api/main.py/middleware or agent/orchestrator.py/review_service.py — slightly broader integration surface.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/28",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "last commit 2026-09-16 by Aburke225 (human), 11 days before capture"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (11 days ago); no releases"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], comments: [], no PR among the repo's 5 PRs closes #28"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction; no AI_POLICY.md/AGENTS.md found"},
      {"name": "labeled-for-newcomers", "grade": "fail", "evidence": "labels: enhancement, safety, tier-2 — no newcomer label"},
      {"name": "repo-widely-used", "grade": "fail", "evidence": "3 stars"},
      {"name": "issue-topic", "grade": "pass", "evidence": "adds FastAPI middleware for per-IP rate limiting — software change"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/16",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "last commit 2026-09-16 by Aburke225 (human), 11 days before capture"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (11 days ago); no releases"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], comments: [], no PR among the repo's 5 PRs closes #16"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction; no AI_POLICY.md/AGENTS.md found"},
      {"name": "labeled-for-newcomers", "grade": "fail", "evidence": "labels: bug, agent, tier-2 — no newcomer label"},
      {"name": "repo-widely-used", "grade": "fail", "evidence": "3 stars"},
      {"name": "issue-topic", "grade": "pass", "evidence": "surfaces failed tool_results from orchestrator to review output — software change"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/9",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "last commit 2026-09-16 by Aburke225 (human), 11 days before capture"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (11 days ago); no releases"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], comments: [], no PR among the repo's 5 PRs closes #9"},
      {"name": "ai-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction; no AI_POLICY.md/AGENTS.md found"},
      {"name": "labeled-for-newcomers", "grade": "fail", "evidence": "labels: enhancement, devops, rag, tier-2 — no newcomer label"},
      {"name": "repo-widely-used", "grade": "fail", "evidence": "3 stars"},
      {"name": "issue-topic", "grade": "pass", "evidence": "content-hash cache for repeated portfolio queries — software change"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

15/20
18/20

**Issue analysis**

issue-20. From `eval-run.txt`: `issue-20  reject  accept   NO     graded accept`. The gold label is `reject` ("one-line feature wish with no spec and a product decision hiding inside"). My rubric's decision is `accept`.

The verdict rule says: "Accept only if every required check is `pass`. A required `fail` or `unclear` rejects the issue." The bundle's required evidence all passes that rule:

- `maintainer-alive`: "2026-08-04 by dwelle" (captured 2026-08-05).
- `repo-in-use`: "archived: no", "last push to any branch: 2026-08-04", "latest release: v0.18.1 (2026-04-21)".
- `unclaimed`: "this issue: assignees: none; linked PRs: none" and "Comments (0 total, first 0 shown)".
- `ai-allowed`: "contribution policy (CONTRIBUTING.md): no statement on AI or contribution tooling".
- `issue-topic`: "Add a new toolbar shape that inserts a fixed company logo (SVG/image)."

No required check failed, so the verdict is `accept`. The gold reject is a scope miss: the rubric has no check for an unsettled spec.

**Check rationale**

`issue-topic`, quoted from `tools/issue-select/rubric.md`:

`| issue-topic | The issue title and body. | The requested work is a software change: application code, tests, docs, tooling, or AI/ML behavior. Fail when the work is primarily hardware: circuits, PCB layout, physical fabrication, or device bring-up with no software change. | required |`

It is `required` because a first contribution here has to be a software change. The pass condition names the kinds of software work that count, and the fail condition is only "primarily hardware" with "no software change."

**Trade-offs**

`issue-topic` gives up unsettled software requests. It only fails "when the work is primarily hardware." issue-20 is the case it misses. From `eval-run.txt`: `issue-20  reject  accept   NO     graded accept`. The gold label is `reject` ("one-line feature wish with no spec and a product decision hiding inside"). The check still passes, because the body says "Add a new toolbar shape that inserts a fixed company logo (SVG/image)." 

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Issue #9 fits my interests and the time I have. It asks for a caching layer so a full RAG pipeline does not rerun on every repeated portfolio query. That is an interesting problem, and the live grading called it a self-contained cache on two files, smaller than #28 and #16.

2. The verdict identified it correctly: `accept`. The rubric accepts this issue. It would not have ranked #9 above the others. #28, #16, and #9 all came back `accept`, and both preferred checks failed the same way (`labeled-for-newcomers` fail, `repo-widely-used` fail, 3 stars), so the rubric treated them the same. Choosing #9 took my own judgment: I wanted an issue that would challenge me.

3. Claiming it should be normal. The verdict records `assignees: []`, `comments: []`, and no PR that closes #9. The work itself is adding some kind of caching layer.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

