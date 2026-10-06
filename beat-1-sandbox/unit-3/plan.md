# Plan: cache a repeated review of an unchanged portfolio

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/9

The request is a cache keyed on the portfolio's content hash, so a second review of an unchanged portfolio returns the stored review instead of re-running the full RAG pipeline.

## Diagnosis

The second post runs RAG because nothing looks up a content hash before `process_review`.

Quoted from the reproduction I posted on that issue (`f89c06f`):

> There is no content-hash lookup before `process_review`.
>
> Both responses came back `200` with `status` `pending` and the same `profile_id`, `32167a41-b0f1-454e-9b3a-70a75fa1c5d9`:
>
> - `d6eba8e3-fdec-4202-8d68-e42fdd5daf63`
> - `2f31ee25-ddbb-4945-a0c2-aba52ee17a93`
>
> The `make run` log then showed this sequence once per review id:
>
> ```text
> review_processing_started
> ingestion_pipeline_completed
> agent_orchestration_completed
> rag_retrieval_completed
> review_processing_completed    overall_score=0.81
> ```
>
> Expected: the second post of an unchanged portfolio returns the stored review and does not run RAG again.
>
> Actual: the second post created a new review and ran RAG again. Each id logged `rag_retrieval_completed` and then `review_processing_completed`.

That log is produced by `create_review_endpoint` in `api/routes/reviews.py`. It always calls `create_review`, then `background_tasks.add_task(process_review, db, review.id, data.profile_id)`. `process_review` in `core/services/review_service.py` then always logs `review_processing_started`, runs ingestion, and calls `_run_rag_retrieval_generation`, which logs `rag_retrieval_completed` and returns `overall_score` `0.81`. The two ids in the repro are two passes through that path.

`IngestedSource.content_hash` is the SHA256 column marked for deduplication. `_run_ingestion_pipeline` inserts the GitHub, portfolio, and resume rows and never sets `content_hash`. No code reads it before `process_review`. `_run_rag_retrieval_generation` does not call `ReviewGenerator`; the `0.81` score is the value that function returns.

## Scope

In scope: one lookup, before `process_review` is queued. Hash the profile fields the ingestion path already reads (`github_username`, `portfolio_url`, `resume_text`). On a later `POST /reviews` for that profile, if those hashes equal the `content_hash` values stored from the completed run, return that completed review and do not call `process_review`.

Out of scope:

- `rag/generator/review_generator.py`. The repro's second `rag_retrieval_completed` comes from `_run_rag_retrieval_generation`, which does not call `ReviewGenerator`. A cache inside the generator would not stop that log line.
- Replacing the placeholder ingestion, agent, or RAG bodies.
- Caching a review that is still `pending` or `processing`. The stored review the issue asks to return is the one that has finished.
- A new cache table or a new API.

## Files

- `core/services/review_service.py` — hash the profile fields, write `IngestedSource.content_hash` while ingesting, and look up the latest `complete` review when the stored hashes still match.
- `api/routes/reviews.py` — call that lookup in `create_review_endpoint` before `create_review`. On a hit, return the stored review and do not queue `process_review`.
- `tests/unit/test_review_service.py` — a unit test that a matching hash returns the completed review, and a changed portfolio URL does not.

## Approach

1. Add `profile_source_hashes(profile)` in `review_service.py`. Build the same three payloads `_run_ingestion_pipeline` already builds (GitHub username, portfolio URL, resume text). SHA256 each payload that is present. A field the profile does not have is omitted, so the repro's profile (no resume) hashes two sources.
2. In `_run_ingestion_pipeline`, set `content_hash` on each `IngestedSource` to the SHA256 of that row's `raw_data` before `db.add`.
3. Add `find_cached_review(db, profile)`. Load this profile's ingested sources and its reviews. Return the latest review with `status == "complete"` only when every current source hash equals the stored `content_hash` for that source. If any hash differs, or any stored hash is null, or no review is `complete`, return `None`.
4. In `create_review_endpoint`, load the profile, call `find_cached_review`, and on a hit return `ReviewResponse` for that review. Do not call `create_review` and do not call `background_tasks.add_task`. On a miss, keep the current create-and-queue path.

## Test plan

Re-run the posted repro on the same setup: Path Review `main` at `f89c06f`, Python 3.13.11 in `.venv`, API on `http://localhost:8000` after `make setup` and `make run`, Postgres from `docker compose` on port 5433, logged in as `user1@example.com`.

Create one profile (`github_username=octocat`, `portfolio_url=https://example.com`) and `POST /reviews` once. Wait until the `make run` log shows `review_processing_completed` for that id. The first post has to finish, because a review still in `pending` is not a stored review. Then post the same body again, with the profile unchanged:

```bash
curl -s -X POST http://localhost:8000/reviews \
  -H "Authorization: Bearer $TOKEN" \
  -H 'Content-Type: application/json' \
  -d "{\"profile_id\": \"$PROFILE\"}"
```

Expected after the fix: the second response is `200`, its `id` is the first review's id, and its `status` is `complete`. The log does not show a second `review_processing_started` or a second `rag_retrieval_completed`.

Control, same profile after that: `PATCH` is not required. Create the comparison by posting a new review only after changing `portfolio_url` on that profile. Expected: a new review id, and the log shows `rag_retrieval_completed` once for that new id. That is the miss the hash is there to allow.

## Risks and unknowns

- Two posts that both arrive before the first `review_processing_completed` will both miss the cache, because no completed review exists yet. The repro's two curls were back to back and both logged a full run. I have not measured that window. The test above waits for the first completion on purpose. I am not treating the overlap as the bug.
- I will hash only the three fields `_run_ingestion_pipeline` reads. I have not checked a profile that also uploads a resume file under a different field name. If one exists, this cache will not see it, and that case stays out of this change.
- Rows ingested before this change have `content_hash` null, so `find_cached_review` returns `None` for them. The repro creates a new profile, so the first run after the change writes the hashes.
- Whether a later replacement of `_run_rag_retrieval_generation` will call `ReviewGenerator` is unknown. It does not today. I am leaving the generator unchanged.

## Deviations

- **Step 2 was wrong about what ingestion stores.** `IngestedSource` has no `raw_data` column, so `IngestedSource(..., raw_data=...)` raises `TypeError`. The old `except` block swallowed it, so ingestion never saved a row and `content_hash` had nowhere to come from. I dropped the `raw_data` argument and set `content_hash` to the SHA256 of the same JSON payload. No migration and no new column. The plan's out-of-scope line is unchanged, but the fix is needed for the cache to work at all.
- **Ingestion now builds its payloads in `_source_payloads(profile)`,** which `profile_source_hashes` also calls, so the stored hash and the lookup hash cannot drift. Ingestion still appends the same payloads and logs the same lines.
- **`find_cached_review` compares the latest stored row per source type.** It also misses when the profile no longer has a source type that was stored earlier (for example a removed resume). That profile keeps missing, which is stale-safe but not optimal.
- **`create_review_endpoint` loads the profile with `get_profile` (owner-checked).** If the profile is not the caller's, it falls through to the old path, so the cache cannot return another user's review.
- **Verified live** on `fix/9-content-hash-review-cache`, API on `localhost:8000`, Postgres on 5433, `user1@example.com`. Profile `octocat` + `https://example.com`: first POST created `89dd38ca-6d1a-4b51-bbb4-5e7deca1c8a8` and the log showed one `review_processing_started` and one `rag_retrieval_completed`. After it completed, the second POST returned the same id with `status` `complete`, and the log showed `review_cache_hit` with no second RAG run. Control: after `PUT /profiles/{id}` changed `portfolio_url` to `https://example.org`, the next POST returned a new id, `40f551c8-784a-46b2-9d6d-7c5c2378be6c`, with one new `rag_retrieval_completed`, and the POST after that hit the cache on the new id. The plan's `PATCH` wording was wrong: the profile update is `PUT` with a JSON body.
- Unit tests in `tests/unit/test_review_service.py` (match returns the completed review; changed URL, null stored hash and no completed review each miss), `ruff`, `black` and `mypy` are clean, and `tests/unit` is 381 passed, 53 xfailed.
