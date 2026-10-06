# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

JaredAung

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/9#issuecomment-6027233493

Reproduced on `f89c06f`: an unchanged profile still starts a second review and a second RAG run. I posted two reviews for profile `32167a41-b0f1-454e-9b3a-70a75fa1c5d9` and got two ids, `d6eba8e3-fdec-4202-8d68-e42fdd5daf63` and `2f31ee25-ddbb-4945-a0c2-aba52ee17a93`. Each id logged `rag_retrieval_completed` and then `review_processing_completed` with `overall_score=0.81`.

The miss is the lookup. `POST /reviews` always creates a review and queues `process_review`, and `process_review` always calls `_run_rag_retrieval_generation`. `IngestedSource.content_hash` is never written or read on that path. The issue names `rag/generator/review_generator.py`; that file is not on this path. `_run_rag_retrieval_generation` returns `0.81` itself and does not call `ReviewGenerator`, so a cache inside the generator would still log a second `rag_retrieval_completed`.

Plan: hash `github_username`, `portfolio_url`, and `resume_text` the same way ingestion already reads them, store each hash on `IngestedSource.content_hash`, and in `create_review_endpoint` look for a `complete` review with those hashes before queuing `process_review`. On a hit, return that stored review. A changed portfolio URL misses the cache and runs the pipeline again. I will re-run the same two posts after the first `review_processing_completed` and confirm the second response reuses the first id and the log has no second `rag_retrieval_completed`.

Two posts that overlap before the first review is `complete` still both run. I have not measured that window, and this change does not cover it.

---

## Your branch

**Branch**

fix/9-content-hash-review-cache

**Evidence**

Before, posted on issue 9 in Unit 2 (`main` at `f89c06f`, no cache). An unchanged profile started a second review and a second RAG run.

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

The `make run` log showed this sequence once per review id:

```text
review_processing_started
ingestion_pipeline_completed
agent_orchestration_completed
rag_retrieval_completed
review_processing_completed    overall_score=0.81
```

After, re-run on `fix/9-content-hash-review-cache` against the API on `http://127.0.0.1:8000` (Postgres from `docker compose` on port 5433, `user1@example.com`). The first post was allowed to reach `complete` before the second post. The profile update is `PUT`, which is the route that exists.

```bash
TOKEN=$(curl -s -X POST http://127.0.0.1:8000/auth/login \
  -d 'username=user1@example.com&password=password1' \
  | python3 -c 'import json,sys; print(json.load(sys.stdin)["access_token"])')

curl -s -X POST http://127.0.0.1:8000/profiles \
  -H "Authorization: Bearer $TOKEN" \
  -F 'github_username=octocat' \
  -F 'portfolio_url=https://example.com'
```

```json
{"id":"620de33a-d241-4374-8d1b-3bbdb3956305","user_id":"90bb40dc-f207-4ac2-9e65-814b39b3301e","github_username":"octocat","portfolio_url":"https://example.com","created_at":"2026-10-07T06:29:38.140023Z","resume_filename":null}
```

```bash
curl -s -X POST http://127.0.0.1:8000/reviews \
  -H "Authorization: Bearer $TOKEN" \
  -H 'Content-Type: application/json' \
  -d '{"profile_id": "620de33a-d241-4374-8d1b-3bbdb3956305"}'
```

```json
{"id":"b0edefd9-ec86-4462-a02b-a79c54e13fc5","profile_id":"620de33a-d241-4374-8d1b-3bbdb3956305","status":"pending","sections":null,"overall_score":null,"error_message":null,"created_at":"2026-10-07T06:29:38.191268Z","updated_at":"2026-10-07T06:29:38.191270Z"}
```

`GET /reviews/b0edefd9-ec86-4462-a02b-a79c54e13fc5/status` then returned `{"review_id":"b0edefd9-ec86-4462-a02b-a79c54e13fc5","status":"complete","progress_pct":0}`.

Same `POST /reviews` again, profile unchanged:

```json
{"id":"b0edefd9-ec86-4462-a02b-a79c54e13fc5","profile_id":"620de33a-d241-4374-8d1b-3bbdb3956305","status":"complete","sections":[{"section_name":"Technical Skills","content":"Detailed feedback on technical skills based on portfolio analysis","confidence":0.85,"suggestions":["Add more detail on AI/ML experience","Include specific technologies and frameworks"]},{"section_name":"Project Experience","content":"Detailed feedback on project experience and impact","confidence":0.8,"suggestions":["Include measurable impact metrics","Add links to project repositories"]},{"section_name":"Career Growth","content":"Feedback on career progression and development","confidence":0.78,"suggestions":["Document learning from each role","Highlight growth in responsibilities"]}],"overall_score":0.81,"error_message":null,"created_at":"2026-10-07T06:29:38.191268Z","updated_at":"2026-10-07T06:29:38.203863Z"}
```

HTTP status `200`. The id is the first review's id.

Control: change the portfolio, then post again.

```bash
curl -s -X PUT http://127.0.0.1:8000/profiles/620de33a-d241-4374-8d1b-3bbdb3956305 \
  -H "Authorization: Bearer $TOKEN" \
  -H 'Content-Type: application/json' \
  -d '{"github_username":"octocat","portfolio_url":"https://example.org"}'
```

```json
{"id":"620de33a-d241-4374-8d1b-3bbdb3956305","user_id":"90bb40dc-f207-4ac2-9e65-814b39b3301e","github_username":"octocat","portfolio_url":"https://example.org","created_at":"2026-10-07T06:29:38.140023Z","resume_filename":null}
```

```bash
curl -s -X POST http://127.0.0.1:8000/reviews \
  -H "Authorization: Bearer $TOKEN" \
  -H 'Content-Type: application/json' \
  -d '{"profile_id": "620de33a-d241-4374-8d1b-3bbdb3956305"}'
```

```json
{"id":"bfc9ceef-5ad7-4ecc-8e18-0402c61fca58","profile_id":"620de33a-d241-4374-8d1b-3bbdb3956305","status":"pending","sections":null,"overall_score":null,"error_message":null,"created_at":"2026-10-07T06:29:56.511904Z","updated_at":"2026-10-07T06:29:56.511905Z"}
```

HTTP status `200`. This id is new.

API log for that run:

```text
review_created                  review_id=b0edefd9-ec86-4462-a02b-a79c54e13fc5
review_processing_started       review_id=b0edefd9-ec86-4462-a02b-a79c54e13fc5
ingestion_pipeline_completed    review_id=b0edefd9-ec86-4462-a02b-a79c54e13fc5 sources_count=2
agent_orchestration_completed   review_id=b0edefd9-ec86-4462-a02b-a79c54e13fc5 sections_count=2
rag_retrieval_completed         review_id=b0edefd9-ec86-4462-a02b-a79c54e13fc5
review_processing_completed     review_id=b0edefd9-ec86-4462-a02b-a79c54e13fc5 overall_score=0.81
review_cache_hit                review_id=b0edefd9-ec86-4462-a02b-a79c54e13fc5
profile_updated                 profile_id=620de33a-d241-4374-8d1b-3bbdb3956305
review_created                  review_id=bfc9ceef-5ad7-4ecc-8e18-0402c61fca58
review_processing_started       review_id=bfc9ceef-5ad7-4ecc-8e18-0402c61fca58
ingestion_pipeline_completed    review_id=bfc9ceef-5ad7-4ecc-8e18-0402c61fca58 sources_count=2
agent_orchestration_completed   review_id=bfc9ceef-5ad7-4ecc-8e18-0402c61fca58 sections_count=2
rag_retrieval_completed         review_id=bfc9ceef-5ad7-4ecc-8e18-0402c61fca58
review_processing_completed     review_id=bfc9ceef-5ad7-4ecc-8e18-0402c61fca58 overall_score=0.81
```

The unchanged second post did not log `review_processing_started` or `rag_retrieval_completed`. The changed portfolio did, once, on the new id.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

20/20

The last score matches `eval-run.txt`: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

pkg-10. From `eval-run.txt`: `pkg-10  unbuildable        reject  reject   yes`. The gold label is `reject`. My rubric's decision is `reject`.

The verdict rule says: "Accept (ready to post and build from) only when every check in the table is `pass`. Reject (hold) when any check is `fail` or `unclear`." `executable` is `required`. Its pass condition says: "A stranger can start from the plan alone. It names a place and a concrete change there. \"Profile and see\", \"poke around\", \"somewhere\", or \"whichever is easier\", with no chosen place and no chosen change, fails."

The candidate plan says: "The git modules on Windows clearly have performance problems, so the plan is to dig into where the time goes and speed them up." Step 1 is "Profile starship on Windows to find the slow parts of the git modules." Step 4 is "Optimize whatever the profiling turns up." The repro already shows `git_status` at `1873ms` against about `350ms` for `git status` itself. The plan never names a change at that module. `executable` fails, so the package is `reject`.

**Check rationale**

`executable`, quoted from `tools/plan-check/rubric.md`:

`| executable | The plan's approach: the place it names and the change it says to make there, read against the files or areas the issue, the thread, or the repro already points at. | A stranger can start from the plan alone. It names a place and a concrete change there. "Profile and see", "poke around", "somewhere", or "whichever is easier", with no chosen place and no chosen change, fails. | required |`

It is `required` because a plan you cannot start is not ready to build from. I kept the quoted phrases instead of a check that fails any plan with no file path. A file path with "optimize whatever shows up" would still pass that weaker check. "Profile and see" is there so pkg-10's "Profile starship on Windows to find the slow parts" fails even though the steps are numbered.

**Trade-offs**

`executable` gives up a plan whose honest next step is to profile before naming a function. pkg-10 is that case: the repro already times `git_status` at `1873ms`, and the plan still only says it will profile and then optimize whatever is hot. I accept that miss. Nothing else moved. From `eval-run.txt`: `categories: clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4` and `agreement: 20/20 scored items  (bar: 18/20: PASS)`. The clear-accept packages stayed `accept`, and the three unbuildable packages stayed `reject`.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
