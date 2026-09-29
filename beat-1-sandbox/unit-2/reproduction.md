# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username** JaredAung

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

---

## Posted upstream

**Claim comment** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/9#issuecomment-5900894674

I'd like to take this as a first contribution. The request is a cache keyed on the portfolio's content hash, so a second review of an unchanged portfolio returns the stored review instead of re-running the full RAG pipeline.

I'll confirm that an unchanged portfolio currently triggers another full run, then look at where that stored review would be returned from `rag/generator/review_generator.py` and `core/services/review_service.py`. I'll post the environment, the steps, and what I actually observe before changing anything.

**Reproduction comment** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/9#issuecomment-5901141211

Reproduced on current `main` (`f89c06f`). An unchanged profile still starts a second review and a second RAG run. There is no content-hash lookup before `process_review`.

Environment: Path Review `main` at `f89c06f` (clean, matching `origin/main`), Python 3.13.11 in the repo `.venv`, API on `http://localhost:8000` after `make setup` and `make run`, Postgres from `docker compose` on port 5433. macOS 26.6.2. Logged in as the seeded account `user1@example.com`.

Steps: created one profile, then posted two reviews for it without changing the profile.

```bash
TOKEN=$(curl -s -X POST http://localhost:8000/auth/login \
  -d 'username=user1@example.com&password=password1' \
  | python3 -c 'import json,sys; print(json.load(sys.stdin)["access_token"])')

PROFILE=$(curl -s -X POST http://localhost:8000/profiles \
  -H "Authorization: Bearer $TOKEN" \
  -F 'github_username=octocat' \
  -F 'portfolio_url=https://example.com' \
  | python3 -c 'import json,sys; print(json.load(sys.stdin)["id"])')

curl -s -X POST http://localhost:8000/reviews \
  -H "Authorization: Bearer $TOKEN" \
  -H 'Content-Type: application/json' \
  -d "{\"profile_id\": \"$PROFILE\"}"

curl -s -X POST http://localhost:8000/reviews \
  -H "Authorization: Bearer $TOKEN" \
  -H 'Content-Type: application/json' \
  -d "{\"profile_id\": \"$PROFILE\"}"
```

Both responses came back `200` with `status` `pending` and the same `profile_id`, `32167a41-b0f1-454e-9b3a-70a75fa1c5d9`:

- `d6eba8e3-fdec-4202-8d68-e42fdd5daf63`
- `2f31ee25-ddbb-4945-a0c2-aba52ee17a93`

`pending` is only the HTTP response. Processing runs after it. The `make run` log then showed this sequence once per review id:

```text
review_processing_started
ingestion_pipeline_completed
agent_orchestration_completed
rag_retrieval_completed
review_processing_completed    overall_score=0.81
```

Expected: the second post of an unchanged portfolio returns the stored review and does not run RAG again.

Actual: the second post created a new review and ran RAG again. Each id logged `rag_retrieval_completed` and then `review_processing_completed`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

19/20
**Package analysis**

pkg-07. From `eval-run.txt`: `pkg-07  accept  reject   NO     failed: disclosure-present`. The gold label is `accept` ("language-priority repro with an English-first control; version delta stated; discloses AI assistance as p5.js's stated policy requires, which is what the conditional-policy pass looks like"). My rubric's decision is `reject`.

The verdict rule says: "Accept only when every required check is `pass`. A required `fail` or `unclear` is reject." `disclosure-present` is `required`. Its pass condition says: "If those sources require a disclosure, each comment being graded includes it."

The repo-facts block requires one: `contribution policy (CONTRIBUTING.md, section "AI Usage Policy"): fully AI-generated contributions are not accepted; assistive AI use is allowed, and the contributor must understand and take responsibility for every change`. The claim comment includes it: "Per the AI usage policy: I used an AI assistant to help me organize this report; I ran and verified every step myself and I understand what I'm reporting." The repro report does not. It ends at "This matches the behavior the issue describes exactly." Because the check says each comment includes the disclosure, that missing sentence is a `fail`, and the package is `reject`. The gold accept treats the disclosure in the claim as enough.


**Check rationale**

`disclosure-present`, quoted from `~/.claude/skills/repro-check/rubric.md`:

`| disclosure-present | Each draft comment, read against an AI-use or other disclosure rule in the repo-facts block (eval) or the repo's contribution docs (live). | If those sources require a disclosure, each comment being graded includes it. If they require none, the check passes. | required |`

It is `required` because a repo that demands a disclosure is not ready to post without one. The second sentence, "If they require none, the check passes," is what I kept instead of always demanding an AI sentence. Most packages say "no stated AI policy," and an unconditional demand would reject those. "Each comment" is there so a disclosure in the claim does not cover a repro report that omits it.

**Trade-offs**

`disclosure-present` gives up a disclosure that appears in only one of the two comments. pkg-07 is the package that changes. From `eval-run.txt`: `pkg-07  accept  reject   NO     failed: disclosure-present`. The gold label is `accept`. The claim says "I used an AI assistant to help me organize this report," and the repro report does not, so the required check fails. The same check still holds the package that discloses nothing: `categories: clear-accept 7/8  disclosure 1/1`, and `pkg-20  reject  reject   yes`.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
