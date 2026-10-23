## Diagnosis and grounding

- Where it lives: Eval: the repro-evidence block (error message, file and line where it fails, the trigger command or input) and the candidate plan's stated cause. Live: the student's posted repro comment on the issue, and the cause section of the draft plan.
- What good looks like: the stated cause names the same error and location the repro evidence shows, and explains why the trigger produces it. If the plan's cause points at a different file, error, or input than the repro shows, it is not grounded.

## Scope

- Where it lives: Eval: the plan's scope statement, its not-in-scope line, and the files or areas it names, read against the issue context. Live: the same parts of the draft plan, read against the issue body.
- What good looks like: the named files or functions are the ones the fault lives in (plus its tests), and the change resolves this issue only. Extra files, refactors, renames, or fixes for other issues that the issue doesn't ask for are scope creep, unless the plan names them as out of scope.

## Executability

- Where it lives: Eval: the plan's approach and order-of-work sections and the files it names. Live: the same in the draft plan.
- What good looks like: a stranger knows which component or module to change and what the change does. If exact functions aren't pinned yet, the plan gives a concrete way to locate them (a log, a trace, a named call path). "Fix the bug in the retriever" is not executable; "add an empty-input check at the start of `KeywordSearcher.index()` in `rag/retriever/keyword_search.py`" is.

## Test plan

- Where it lives: Eval: the plan's test plan, read against the repro-evidence block's steps and artifacts. Live: the draft plan's test plan, read against the posted repro comment's commands.
- What good looks like: the test plan names an observation that differs between broken and fixed, tied to the reproduced trigger: re-running the repro command, or a named test that fails now and passes after. "Run the tests" or "verify it works" names nothing that would show the bug is gone.

## Honesty

- Where it lives: Eval: the plan's risks or unknowns section, plus any claim about cause, side effects, or certainty anywhere in the plan; deviation notes if present. Live: the same in the draft plan; mid-build deviations are recorded in the plan's deviations section and, if the posted intent changed, in a thread update.
- What good looks like: a diagnosis may be a reasoned inference, as long as it rests on what the repro and its controls show. False confidence is a guarantee the evidence can't support ("this fixes every case", "nothing else is affected"), a claim the evidence contradicts, or a risk the plan's own approach creates that it doesn't mention.

## Comms

- Where it lives: Eval: the plan comment, read against the thread highlights (maintainer asks, decisions, prior attempts, who is working on what) and the repo-facts block (issue and PR templates, contributing asks, AI-use policy). Live: the draft comment, read against the issue thread on GitHub and the repo's CONTRIBUTING, templates, and policy docs.
- What good looks like: the comment responds to what the thread actually says (follows a maintainer's requested approach, respects a decision, acknowledges a prior attempt if relevant) and does what the repo's conventions ask. Boilerplate that could be posted on any issue is not thread-aware.
- AI disclosure: treat every package as AI-assisted work. If the AI policy explicitly requires disclosure, look for the disclosure in the comment itself, with whatever details the policy names (such as the tool and the extent of assistance).