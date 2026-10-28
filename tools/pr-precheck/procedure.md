## Read order

1. Read the issue first. Note the reported behavior and the trigger.
2. Read the plan second: note its in-scope and not-in-scope lines, the files or functions it names, its test plan, and every deviation note. The plan must come before the diff, because every fidelity check measures the diff against it; reading the diff first lets the diff set the standard.
3. Read the repo facts and thread third: note each PR template section, the contributing asks (including the checks the repo says to run), the AI-use policy and whether it explicitly requires disclosure (and what details), any house rule from scope.md (live mode), and any explicit maintainer direction.
4. Read the diff and the commit list fourth. List every changed file and, for each, what its hunks do.
5. Read the test evidence fifth. Note each command shown and its output.
6. Read the description last, after the diff and evidence, so its claims are checked against what you've already seen rather than framing it. List each claim it makes.

## Evidence gathering

Record each pairing below before grading, citing where each fact came from.
- Diff matches plan: the changed-file list (step 4) next to the plan's scope and deviation notes (step 2). Mark each file in-scope, covered by a deviation, or unplanned; mark each promised change present or missing.
- Description matches diff: each description claim (step 6) next to the diff hunk or evidence that confirms or contradicts it, plus any diff change the description never mentions.
- Before/after shown: the before output and the after output (step 5) next to the plan's test plan and the issue's trigger (steps 1–2).
- Repo checks run: the checks the repo names (step 3) next to the check outputs shown or disclosed as not run (step 5).
- Diff is reviewable: any hunk in step 4 that is debug output, dead or commented-out code, formatting-only churn, or unrelated to the fix.
- Template filled: each template section (step 3) next to the description's content for it.
- AI disclosure: the policy's requirement (step 3) next to any disclosure line in the description.
- Thread direction honored: each maintainer direction (step 3) next to what the PR does about it.
In live mode, gather from the locations in references/evidence-guide.md: plan.md, `git diff main...HEAD`, `git log main..HEAD --oneline`, the draft description file, the captured test output, the issue thread, and the repo's PR template and CONTRIBUTING.md.

## Check execution

1. Run the checks in rubric order. Grade each only against its recorded pairing, using its pass condition as written.
2. Grade each check pass, fail, or unclear. Use unclear only when the evidence the check needs is genuinely absent from the package. If the evidence is present, decide.
3. If the package has no material for a check whose pass condition can still be met (no AI policy, no maintainer direction), grade pass and say why.
4. Write one evidence line per check, quoting or citing the specific fact that decided it.
5. Don't re-read the whole package for a check unless its recorded pairing is missing a fact the pass condition needs; then re-read only the part the evidence guide names for it.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required check is pass.
2. Any required check graded fail or unclear makes the verdict reject.
3. The deciding check is the first failing (or unclear) required check in rubric order. In the summary, quote its evidence line as the reason for the verdict, and list the other failing checks after it. If the verdict is accept, there is no deciding check.
4. End with the JSON block exactly as SKILL.md specifies: every check's name, grade, and evidence, then the verdict, with nothing after it.