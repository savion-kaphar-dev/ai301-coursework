## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Alive | Last 10 commits on the default branch (Code tab commit list, or Insights → Commits) | At least one commit within the last 90 days | required |
| In-Use | Star count and open issue count, shown in repo header | ≥50 stars, OR ≥5 open issues with activity (comments/labels) in the last 90 days | required |
| Scope | Issue title and body text under the specific issue in the Issues tab | Describes one concrete, bounded piece of work — what's wrong or what's wanted — specifically enough that someone could start without asking the reporter to clarify. Judge by what the body actually says, not by its bug/feature label; a short informal report is fine, and formal repro-steps/expected-vs-actual writeups or named files are a plus, not a requirement. A trailing "etc." after named examples, or several possible causes/fixes offered for the same underlying problem, still count as one bounded item. Fails only if the issue itself is open-ended: an ongoing initiative, a running list/index of other issues, or "help wanted, details TBD" with no specific ask | required |
| Unclaimed | Assignees field in issue sidebar, comment thread, linked PRs shown above issue body | No assignees; no comments within the last 60 days claiming the issue; no open linked PR | required |


## Verdict rule

Accept only if every required check passes. If any required check is `unclear`, treat it as fail (reject) — do not guess in the maintainer's favor. Preferred checks never flip accept/reject; use them only to rank issues that already passed all required checks (more preferred checks passed = higher priority).
