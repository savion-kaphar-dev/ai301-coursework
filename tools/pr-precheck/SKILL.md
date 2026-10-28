---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: is this pull request ready to submit?

A PR package is a candidate pull request: its title, its description, its commits, its diff, and its test evidence. Read it against two things: the plan it claims to implement (including that plan's recorded deviations) and the issue that plan belongs to, along with the repo's stated standards (PR template, contributing rules, AI-use policy).

Grade one package per run. Do not review the code's style, suggest improvements beyond what the checks ask, or answer any other question. If asked to grade more than one package, or something that is not a PR package, say so and stop.

## Inputs and modes

Determine the mode first. If the input is an eval package bundle, use eval mode. Otherwise use live mode.

**Live mode** grades the student's own submission before it goes out. Gather these inputs:
- **The plan:** the student's `plan.md`, including its Deviations section, from the path they give. A house-chain student gives the house plan instead.
- **The diff:** everything the branch changes relative to the repo's default branch. Produce it by running `git diff main...HEAD` (three dots) from the student's working copy, on their fix branch. Also run `git log main..HEAD --oneline` for the commits.
- **The draft PR:** the title and description from the file the student names.
- **The test evidence:** whatever the description or a named file shows (repro before and after, the repo's own checks and their output).
- **The issue:** the issue URL the student gives. Gather issue-side evidence from the real repo: the issue thread, the student's posted repro and plan comments, the PR template (for example `.github/PULL_REQUEST_TEMPLATE.md`), and the repo's contributing and AI-use policy docs. A house-chain student reads the house repro pack instead of their own repro comment.

If a required live input is missing (no plan path, no branch, no draft), say which one and stop rather than grading part of a package.

**Eval mode** treats the bundle as the whole world. Take every fact from the bundle text. Fetch nothing, run no commands, and read nothing outside the bundle. Always grade a complete package: run every check in rubric.md and apply the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else.
- If its `Repo:` line still holds a placeholder (anything in angle brackets, such as `<ORG>/<PATH-REVIEW-REPO>`), stop without grading. Tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo.
- If the PR does not target the scoped repo (the issue or the base repository is somewhere else), refuse to grade and say why.
- Apply the house rules scope.md lists as part of the standards the checks read against.
- Never guess a scope.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after grading, read `voice-guide.md` and hold the outgoing PR text (the title and the description) against its rules. For each rule the draft breaks, report the rule and the line that breaks it in the summary, under "Voice-guide notes." These notes never change the verdict on their own, because voice is personal and the rubric decides readiness; only a rubric check that reads the voice guide can affect the verdict.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read these components from this directory before grading, and use them as follows:
- `rubric.md` defines the checks and the verdict rule. Grade only those checks, with their pass conditions as written.
- `references/evidence-guide.md` maps where each evidence family lives, in a bundle and in live mode. Use it to locate the evidence each check names.
- `procedure.md` gives the operating steps: read order, evidence gathering, check execution, and verdict assembly. Execute it as written, in order.

If the procedure is silent on a step you need, do not improvise around it. Take the narrowest reading that the rubric supports, and report the gap in the summary under "Procedure gaps."

If `rubric.md` has no checks or no verdict rule, or `procedure.md` has no steps (only template comments), refuse to grade. Say which file is empty and that it must be filled first. Never invent checks at runtime.

## Verdict and output

The verdict is binary: `accept` means ready to submit, and `reject` means hold. There is no third verdict, no score, and no "accept with reservations." Put reservations in check evidence lines.

Before the JSON, you may give a short readable summary: each check's grade with one line of evidence, then the voice-guide notes and procedure gaps in live mode.

End the reply with the fenced JSON block below, valid and last, with nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first.** Grade no check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- **Grade the thing, not the polish.** Read the artifact itself against the plan, the issue, and the stated standards. A terse but complete PR can be ready; a polished, confident one can be hiding drift. Never grade formatting, length, or tone.
- **The rubric decides.** If a check passes by its stated condition but feels wrong, it still passes. Note the concern in the evidence line; the fix belongs in the rubric, not in this run.
- **The procedure decides how.** Follow `procedure.md` as written, and report its gaps rather than inventing steps.
- **Unclear defaults to fail.** Apply the rubric's verdict rule to `unclear` grades. Where the rule is silent, treat an unverifiable claim as failing: a PR you cannot verify from the package is not ready to submit.