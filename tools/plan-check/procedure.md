## Read order

1. Read the issue context first. Note the reported behavior and anything the reporter says about cause or expected behavior.
2. Read the repro evidence second. Note the exact error, the file and line it fails at, and the trigger. This pins down what any diagnosis must explain, so it must be read before the plan, not after.
3. Read the thread highlights and the repo-facts block third. Note every maintainer ask or decision, and every stated convention or AI-use requirement. Note whether the AI policy explicitly requires disclosure, and what it says the disclosure must include. These are what the comms check measures against.
4. Read the candidate plan fourth, then the plan comment last. Reading them after the evidence keeps the plan's own framing from setting the standard.

## Evidence gathering

For each check, record the fact named below before grading anything, citing where it came from.
- Diagnosis grounded: the plan's stated cause, next to the error and location from step 2.
- Targets the cause: the plan's proposed change, next to the failure point from step 2.
- One bounded change: every file, function, or area the plan says it will touch, and its not-in-scope line.
- Stranger could start: the named file(s) and function(s), and the one-sentence description of the change.
- Test plan observable: the observation the test plan names, next to the repro trigger from step 2.
- Unknowns stated honestly: each claim of certainty in the plan, and whether the repro evidence backs it.
- Comment fits thread and repo: each maintainer ask and convention from step 3, and whether the comment meets it.
- Comment states the plan: the change and the check the comment describes, next to the plan's.
In live mode, gather from the locations in references/evidence-guide.md.

## Check execution

1. Run the checks in rubric order. Grade each one only against the evidence recorded for it, using its pass condition word for word.
2. Grade each check pass, fail, or unclear. Use unclear only when the evidence for that check is genuinely absent from the package (for example, no thread highlights exist), not when it's hard to judge; if the evidence is present, decide.
3. If a check's evidence is absent because the package doesn't contain that part, and the pass condition can still be met without it (for example, no maintainer asks to follow), grade pass and say why.
4. Write one line of evidence per grade, quoting or citing the specific part of the package it rests on.
5. Don't re-read the whole package for a check unless its recorded evidence is missing a fact the pass condition needs.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required check is pass.
2. Any required check graded fail or unclear makes the verdict reject. Preferred checks never change the verdict.
3. In the output, quote the evidence line for each failing required check (the deciding checks). If the verdict is accept, no deciding check is quoted.
4. End with the fenced JSON block in the format SKILL.md specifies, with every check's name, grade and evidence, then the verdict.