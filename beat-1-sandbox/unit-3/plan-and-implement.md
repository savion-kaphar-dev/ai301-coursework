# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

savion-kaphar-dev

**Plan comment**

[PLAN](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/68#issuecomment-6367078173)

Following my repro above (commit 99673c7), here's my plan: add an empty-list check at the start of `KeywordSearcher.index()` in `rag/retriever/keyword_search.py`, so an empty `chunks` list resets the index and returns before it ever reaches `BM25Okapi`. `search()` already returns `[]` in that state, so the two will match. I'll also remove the `xfail` marker from `test_empty_index`. Per CONTRIBUTING.md I also checked `pyproject.toml` for related suppressions; there's no mypy override for `keyword_search`, so the xfail marker is the only one. To check it, that test currently fails with `ZeroDivisionError` under `--runxfail`; after the change it should pass as a normal test, with the other 16 tests in the file still passing. One thing I'm leaving out of scope: a non-empty list where every chunk's text is empty might also break BM25's scoring, but that's a separate case from this issue, so I'll note it in the PR rather than fix it here. I’ll work on branch `fix/68-empty-index`. Happy to adjust if you’d prefer a different approach, and thanks for reviewing!

---

## Your branch

**Branch**

fix/68-empty-index

**Evidence**

Before (on `fix/68-empty-index`, before the change, running the Unit 2 repro command):

```
$ pytest tests/unit/test_keyword_search.py --runxfail
FAILED tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index - ZeroDivisionError: division by zero
1 failed, 16 passed in 0.48s
```

After (guard added to `KeywordSearcher.index()`, xfail marker removed):

```
$ pytest tests/unit/test_keyword_search.py
17 passed in 0.30s
```

## Eval iterations

**Run history**

1. 18/20
2. 20/20
3. 20/20 (final run, matches the committed eval-run.txt)

**Package analysis**

pkg-20 (thread-convention). Gold label: reject. My rubric decided accept in run 1 and reject in my final run.

In run 1, every check passed, and the comms check's evidence said: "package shows no AI use, so no disclosure is shown to be required (tension noted)." The repo's AI policy says all AI usage must be disclosed, stating the tool used and the extent of assistance, and the plan comment has no disclosure. My first comms check only said to check "any required AI disclosure," so the grader decided disclosure only applied if the package showed AI use. I added "Treat every package as AI-assisted work" and spelled out that when the policy explicitly requires disclosure, the comment must contain it with the details the policy names. After that, pkg-20 is rejected on the comms check, matching gold.

**Check rationale**

```
| Comment fits thread and repo | The plan comment, read against the thread highlights (maintainer asks, decisions, prior attempts) and the repo-facts block (templates, contributing asks, AI policy). Treat every package as AI-assisted work. | The comment follows what maintainers asked for in the thread and what the repo's stated conventions require, and does not contradict a maintainer decision. If the AI policy explicitly requires disclosing AI use, the comment must contain that disclosure, including any details the policy names (such as the tool and the extent of assistance). A policy that only welcomes AI or asks for understanding requires nothing visible. Fail if a maintainer ask, a stated convention, or a required disclosure is missing or contradicted. | required |
```

It reads this way because my first version let pkg-20 through. The grader treated the disclosure rule as conditional on the package showing AI use. Adding "Treat every package as AI-assisted work" removes that loophole, and requiring "any details the policy names (such as the tool and the extent of assistance)" stops a vague one-word disclosure from passing a policy that asks for more. I kept the line "A policy that only welcomes AI or asks for understanding requires nothing visible" so the check doesn't fail repos whose policy asks for nothing.

**Trade-offs**

The same revision also loosened two checks for pkg-14, a clear-accept my rubric wrongly rejected: "Stranger could start" now accepts a named module plus a concrete way to locate the exact functions, and "Unknowns stated honestly" now accepts a diagnosis inferred from the repro's controls. Loosening risks passing plans that should be held, so I re-ran with `--only pkg-14,pkg-20,pkg-04,pkg-10,pkg-17,pkg-01,pkg-02`:
- canaries pkg-10 and pkg-17 (unbuildable) for the looser "Stranger could start"
- canary pkg-01 (wrong-cause) for the looser "Unknowns"
- canaries pkg-04 (the other thread-convention) and pkg-02 (clear-accept) for the stricter comms check

All 7 agreed, and the next full run was 20/20. One case I accept it may miss: my procedure doesn't say to read repo docs the package doesn't mention. In live mode, one plan-check run passed my plan and a later run caught that CONTRIBUTING.md also asks to remove related suppressions from `pyproject.toml`, so whether that doc gets read can vary between runs.