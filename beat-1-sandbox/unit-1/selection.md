# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[https://github.com/codepath/pathreview-ai301-fa26-howard/issues/71]

**Verdict output**

```
├──────────────────────────────────┼──────────────────────────────┼─────────────────────────────────────────────────────────────────────────┼─────────┤
│ #54 – Resume section detection   │ Pass — bounded, repro steps, │ Pass — no assignee, no PR; the one comment is a student asking to claim │ Accept  │
│ whitespace bug                   │  named file                  │  it, which the house rule says doesn't block                            │         │
└──────────────────────────────────┴──────────────────────────────┴─────────────────────────────────────────────────────────────────────────┴─────────┘

Ranking note: scope.md's fit profile is still a placeholder ("Write a few sentences here."), so there's no student-specific signal to rank #71 vs #54 on. Listed below in the order they'd likely suit a newcomer looking for the smaller lift: #71 has a 1–2 hour estimate and a very narrow, mechanical fix (de-indent a test fixture); #54 also carries a good first issue label and comes with explicit repro code, but touches parsing logic across three failing tests. Fill in the fit profile in scope.md for a real ranking next time.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/71",
    "checks": [
      {"name": "Alive", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16T21:42:18Z, 13 days before capture date 2026-09-29"},
      {"name": "In-Use", "grade": "pass", "evidence": "75 open issues with labels/comments added as recently as 2026-09-27"},
      {"name": "Scope", "grade": "pass", "evidence": "Body names exact files (test_readme_parser.py, readme_parser.py), one concrete fix (remove 8-space indentation), 1-2h estimate"},
      {"name": "Unclaimed", "grade": "pass", "evidence": "0 comments, no assignees, timeline shows only label/rename events, no cross-referenced PR"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/54",
    "checks": [
      {"name": "Alive", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16T21:42:18Z, 13 days before capture date 2026-09-29"},
      {"name": "In-Use", "grade": "pass", "evidence": "75 open issues with labels/comments added as recently as 2026-09-27"},
      {"name": "Scope", "grade": "pass", "evidence": "Body pinpoints `_detect_sections()` in resume_parser.py, includes runnable repro code and named failing tests"},
      {"name": "Unclaimed", "grade": "pass", "evidence": "No assignees, no open linked PR; sole comment is a student team asking to claim, which the Path Review house rule says does not block"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/68",
    "checks": [
      {"name": "Alive", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16T21:42:18Z, 13 days before capture date 2026-09-29"},
      {"name": "In-Use", "grade": "pass", "evidence": "75 open issues with labels/comments added as recently as 2026-09-27"},
      {"name": "Scope", "grade": "pass", "evidence": "Body names exact files (keyword_search.py, test_keyword_search.py), one concrete fix, 2-4h estimate"},
      {"name": "Unclaimed", "grade": "fail", "evidence": "Timeline shows cross-referenced open PR #73 ('Fixes #68'), body: 'Fixes #68' — still open/unmerged"}
    ],
    "verdict": "reject"
  }
]
```

---

## Eval iterations

categories: claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 0/1  scope 4/4
agreement: 18/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)

**Run history**

[
categories: claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 0/1  scope 4/4
agreement: 18/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)
]

**Issue analysis**

[Rubric's decision: accept
Gold label: reject (category: policy)

Why the rubric produced accept:


| Check      | Grade | Evidence |
|------------|-------|----------|
| Alive      | ✅ Pass | Last push 2026-08-12 (same day as capture); last 5 commits are all within days of each other |
| In-Use     | ✅ Pass | 2,766 stars (≥50 threshold) |
| Scope      | ✅ Pass | Body describes one concrete UI change — factor in-progress books into the reading-goal progress bar, with a worked example (1/10 books + 20% into book 2 = ~12%) |
| Unclaimed  | ✅ Pass | No assignees, no linked PRs; the one prior claim attempt (jrings, "I've started to look at this...") was 2024-09-19 — well outside the 60-day claim window measured from the 2026-08-12 capture date |

All four required checks pass → the rubric's verdict rule (accept only if every required check passes) accepts it.

Why gold says reject: none of that reasoning is wrong on its own terms — the disagreement isn't a threshold miss on an existing check. The repo's CONTRIBUTING.md states outright: "We do not accept AI-generated code or documentation." That's an outright ban per the evidence guide's "fifth surface," and the rubric currently has no check that reads the contribution-policy line at all, so nothing in the table can catch it. This is the same gap behind the policy 0/1 category floor miss from the full run.]

**Check rationale**

[Describes one concrete, bounded piece of work — what's wrong or what's wanted — specifically enough that someone could start without asking the reporter to clarify. Judge by what the body actually says, not by its bug/feature label; a short informal report is fine, and formal repro-steps/expected-vs-actual writeups or named files are a plus, not a requirement. A trailing "etc." after named examples, several possible causes/fixes for the same underlying problem, or several concrete sub-tasks/files for one specified initiative, still count as one bounded item — "bounded" means every part of it is spelled out, not that it touches only one file or one action. Fails only if the issue itself is open-ended: an ongoing initiative, a running list/index of other issues, or "help wanted, details TBD" with no specific ask. 
This check serves to determine whether the issue's scope is reasonable to approach. The first sentence is a quick, concise statement that catches most cases, and the following sentences are addenda that further refine the bounds and qualifications of the initial statement.]

**Trade-offs**

[The scope causes issue four (which the gold labels as a valid issue) to be rejected. This may be because the check is looking for more information about the issue that it can't find due to the brevity of the issue description.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. This issue seemed reasonably short while still taking some time -- it has an estimated effort of 1-2 hrs. It also strikes me as a reasonable issue in terms of scope, with a little bit of challange.
2. The AI tool correctly noted that the scope of this issue seems perfect for me, however, what it likely didn't take into account is that the issue also presents theorized causes for the issue, making it even more manageable.
3. It seems like a relatively straightforward issue to claim with a little bit of busywork behind it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
