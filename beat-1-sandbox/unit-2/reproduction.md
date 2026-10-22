# Unit 2 — Claim and Reproduce

## Your identity upstream

**GitHub username**

savion-kaphar-dev

---

## Posted upstream

**Claim comment**

[CLAIM COMMENT](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/68#issuecomment-6071339230)

Thanks for filing this. I'd like to work on it.

The issue reports that `KeywordSearcher.index([])` raises a `ZeroDivisionError` from inside rank-bm25 when the empty tokenized corpus is passed to `BM25Okapi`, while `search()` already handles the empty case by returning an empty list. The covering test in `tests/unit/test_keyword_search.py` is currently marked `xfail` (H-01).

My next step is to set up the project locally following the repo's docs, then try to reproduce this two ways: by running the xfail-marked test without the marker, and by calling `index([])` directly. Realistically, I'll post a repro report here once I have the project running, with my environment (Python and rank-bm25 versions), the exact steps, and the output I observe, including the full traceback if it does raise.

If I can reproduce it, I intend to fix `index()` for the empty corpus and remove the xfail marker in the same pull request, as the issue asks.

**Reproduction comment**

[REPRO COMMENT](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/68#issuecomment-6319080254)

Reproduced issue #68: calling `KeywordSearcher.index([])` crashes with a `ZeroDivisionError`. With an empty corpus, rank-bm25 tries to find the average document length by dividing the total word count by the number of documents (0), and `index()` passes the empty list in without checking it first.

**Environment:** Python 3.14.7 · rank-bm25 0.2.2 · pytest 9.1.1 · macOS · commit `99673c7`

**Steps, From a clone of my fork:**
clone → check out `99673c7` → set up the venv per the README → run:
```
pytest tests/unit/test_keyword_search.py --runxfail
```

**Expected:** `index([])` returns without raising, consistent with `search()` returning an empty list on empty input
**Actual:** `ZeroDivisionError: division by zero` raised inside rank-bm25 (1 failed, 16 passed)

```
$ pytest tests/unit/test_keyword_search.py --runxfail
>       searcher.index([])
E       ZeroDivisionError: division by zero
```

<details><summary>Full pytest output</summary>

```
collected 17 items

tests/unit/test_keyword_search.py ........F........                    [100%]

=================================== FAILURES ===================================
_____________________ TestKeywordSearcher.test_empty_index _____________________

    def test_empty_index(self, searcher):
        """Test searching on empty index."""
>       searcher.index([])

tests/unit/test_keyword_search.py:140:
rag/retriever/keyword_search.py:25: in index
    self.bm25 = BM25Okapi(tokenized_corpus)
.venv/lib/python3.14/site-packages/rank_bm25.py:83: in __init__
    super().__init__(corpus, tokenizer)
.venv/lib/python3.14/site-packages/rank_bm25.py:27: in __init__
    nd = self._initialize(corpus)

self = <rank_bm25.BM25Okapi object at 0x10815c050>, corpus = []

>       self.avgdl = num_doc / self.corpus_size
E       ZeroDivisionError: division by zero

.venv/lib/python3.14/site-packages/rank_bm25.py:52: ZeroDivisionError
=========================== short test summary info ============================
FAILED tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index - ZeroDivisionError: division by zero
========================= 1 failed, 16 passed in 0.34s =========================
```

</details>

Next, I'll open a PR from my fork that makes `index()` handle an empty corpus and removes the `xfail` marker on `test_empty_index`.

## Eval iterations

**Run history**

1. 19/20 (2026-10-08, bar 18/20, PASS)
2. 20/20 (2026-10-21, bar 18/20, PASS), final run, matches the committed eval-run.txt

**Package analysis**

pkg-09. My rubric decided `accept` in the final run; the gold label is `accept` (clear-accept). The gold note reads: "honest cannot-reproduce: real attempt at the argument-size reordering with marker-order artifacts, names what differed (uniform name lengths, 2 MiB ARG_MAX) and what a triggering setup likely needs".

My rubric read it as a pass because of the Honest outcome check, which says "A cannot-reproduce that shows a real attempt and names what differed is a pass." pkg-09 didn't reproduce the bug, but it shows a real attempt with artifacts and names exactly what differed from the triggering setup, so it doesn't overclaim. In my first run the same package was rejected (failed: Honest outcome, Next step concrete), even though the rubric was unchanged (same rubric hash, fe8155963f030804, in both runs). That shows pkg-09 sits on the line between "honest cannot-reproduce" and "didn't reproduce," and the grading model can land on either side.

**Check rationale**

> **Next step concrete**: States a specific next step (what the author will try or fix next, or what a maintainer could check). Weight: preferred

It's weighted `preferred` rather than `required` because a report can be complete proof without one. The environment, steps and artifact are what let a stranger check the bug. A next step makes the report more useful, but a strong reproduction shouldn't be rejected only for leaving it out. The "or what a maintainer could check" part is there so a cannot-reproduce report can still earn it, by pointing to what a triggering setup would need.

**Trade-offs**

Nothing in the skill changed between my two runs, and I know because the rubric hash is fe8155963f030804 in both, and skill/ is identical in the two commits (ecd39f1 and 88b3577). The one difference in results, pkg-09 flipping from reject to accept, came from run-to-run variation in the grading model, not from a revision. The trade-off I accept is that the Honest outcome check's "real attempt and names what differed" condition is a judgment call, so borderline cannot-reproduce packages like pkg-09 can flip between runs. My score can vary by one package on reruns even with the same rubric.
