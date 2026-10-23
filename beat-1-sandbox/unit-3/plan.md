# Plan: issue #68, KeywordSearcher.index([]) raises ZeroDivisionError

## Diagnosis
`KeywordSearcher.index()` (rag/retriever/keyword_search.py) passes its tokenized corpus straight to `BM25Okapi`. With an empty list, rank-bm25 computes the average document length as total words / number of documents = 0 / 0 and raises `ZeroDivisionError` (rank_bm25.py:52, reached from keyword_search.py:25). My repro showed this on commit 99673c7 with `pytest tests/unit/test_keyword_search.py --runxfail`. `search()` already handles the empty state by returning `[]`; `index()` doesn't.

## Scope
One bounded change: make `index()` handle an empty `chunks` list without calling `BM25Okapi`.
- In scope: `KeywordSearcher.index()` in rag/retriever/keyword_search.py, and removing the `@pytest.mark.xfail` marker on `test_empty_index` in tests/unit/test_keyword_search.py.
- Not in scope: changes to rank-bm25, to `search()`, or to how chunks are produced upstream; the separate case of non-empty chunks whose text is all empty (see Unknowns).

## Approach
1. At the start of `index()`, if `chunks` is empty: set `self.chunks = []` and `self.bm25 = None`, log that the index is empty, and return without building BM25. Resetting `self.bm25` keeps a previously built index from going stale.
2. Leave the non-empty path unchanged.
3. Remove the `xfail` marker from `test_empty_index`. It's `strict=True`, so once the fix works, leaving it in would fail the run.
4. Per CONTRIBUTING.md, check `pyproject.toml` for suppressions tied to this issue. I checked: there's no mypy override for `rag.retriever.keyword_search`, so the `xfail` marker is the only suppression to remove.

## Test plan
- Before: `pytest tests/unit/test_keyword_search.py --runxfail` fails `test_empty_index` with `ZeroDivisionError`.
- After: `pytest tests/unit/test_keyword_search.py` passes all 17 tests, with `test_empty_index` passing as a normal test (no xfail), and the other 16 still passing.
- Also check `search()` after `index([])` returns `[]` (the test already asserts this).

## Risks and unknowns
- A non-empty list where every chunk's text is empty would give BM25 all zero-length documents, which may also break its scoring. I haven't tested this; it isn't the behavior in #68, so I'm leaving it out of scope and will mention it in the PR as a possible follow-up.
- Other callers of `index()` might rely on the old behavior (an exception). I'll check where `index()` is called before opening the PR.

## Deviations
- Nothing changed; the plan held. The guard went in at the start of index() as planned, the xfail marker was the only suppression (no pyproject.toml entry), and the caller check found no code outside the tests calling index().