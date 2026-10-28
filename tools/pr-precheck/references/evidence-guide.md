## Plan fidelity (harness category: silent-drift)

- Where it lives: Eval: the plan-context block's scope pair (in-scope, not-in-scope), its named files, and any deviation notes, read against the candidate PR's diff and the description's claims. Live: plan.md and its Deviations section, read against `git diff main...HEAD` and the draft description.
- What good looks like: every changed file falls inside the plan's boundary or a deviation note, every promised change is present or its absence is noted, and the description claims exactly what the diff does. Silent drift runs both ways: unplanned files or features with no note, or a promised change missing with no note. A description claiming fidelity the diff contradicts is drift too.

## Test evidence (harness category: not-tested)

- Where it lives: Eval: the PR's test-evidence section, read against the plan-context block's test plan and the reproduction's steps, plus the repo-facts block's named checks. Live: the test output in the draft description (or a captured file the student names), read against plan.md's test plan, the posted repro comment, and the checks CONTRIBUTING.md or the Makefile names.
- What good looks like: the reproduced trigger (or named test) is shown failing before and passing after, with commands and output, and the repo's own checks are shown with their outcome (or one is named as not run, with a reason). "Tests pass" or "verified locally" with nothing shown proves nothing observable.

## Diff quality (harness category: unreviewable)

- Where it lives: Eval: the candidate PR's unified diff and commit list. Live: `git diff main...HEAD` and `git log main..HEAD --oneline`.
- What good looks like: a reviewer sees the fix and nothing else. Debris tells: print or debug statements, commented-out blocks, dead code, unrelated renames, whitespace or formatting churn outside the changed lines, and edits to files the change doesn't need.

## Standards and comms (harness category: standards-wall)

- Where it lives: Eval: the repo-facts block's PR template sections, contributing instructions, and AI-use policy, plus the thread highlights for maintainer direction, read against the description. Live: the repo's `.github/PULL_REQUEST_TEMPLATE.md`, CONTRIBUTING.md, any AI policy doc, scope.md's house rules, and the issue thread, read against the draft description.
- What good looks like: every template section is filled with content specific to this change, the AI disclosure is present when the policy or a house rule explicitly requires it (treat every package as AI-assisted work), and explicit maintainer direction is followed or the departure explained. Boilerplate, leftover template text, or a missing required disclosure is a visibly ignored ask. (Whether the description's claims match the diff belongs to plan fidelity, above.)