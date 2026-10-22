# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment record (OS, tool/app version, and any runtime, driver, or build profile the issue's behavior depends on), read against the environment the issue names and the repo-facts block's bug-report template asks | The report states the environment its artifacts were produced in, with the items the issue's behavior plausibly depends on, and any difference from the issue's stated target (version, OS, shell, build profile) is named rather than silent. Fail if no environment is recorded, or a deviation from the issue's target is present and not acknowledged. | required |
| Steps followable | The repro report's commands and steps, read as a stranger starting from a clean machine | Every step needed to reach the trigger is present, in order, from starting state to the trigger, and uses only things a stranger can get (public repos, shared configs, inputs given inline or described precisely enough to recreate, such as a minimal file described by its relevant contents, or the issue's own example). Background state (an already-populated environment, say) need only be stated if it plausibly changes the trigger. Fail if a trigger step is skipped or changed, or a step depends on private code or config that is not provided. | required |
| Behavior matches issue | The report's artifacts (output excerpts, logs, exit codes, screenshots) read against the failure the issue describes | The artifact itself shows the issue's specific behavior (same error, panic, exit code, or symptom), produced with the issue's trigger. Fail if the artifact shows an adjacent behavior (a different error, a graceful failure instead of a crash, a modified input, a different version's behavior) or only shows that the tool runs. A control run showing the contrast is a plus but not required. | required |
| Honest outcome | The report's stated conclusion against what its artifacts show, including the claim comment's assertions about the cause, scope, or certainty | Every claim is backed by a shown artifact: the conclusion states what was observed and no more. A cannot-reproduce that shows a real attempt and names what differed is a pass. A brief side observation (such as a control run) that matches the issue's or owner's own description is acceptable without its own transcript; the main reproduced behavior must be shown. Fail if it asserts reproduction without artifacts, diagnoses a cause or generalizes to other versions/platforms with no shown evidence, or narrates an artifact as something it is not. | required |
| Claim specific and honest | The candidate claim comment read against the issue | The claim names what the author will actually do on this issue (a concrete intent or plan tied to the issue's content) and promises nothing it cannot back (no guaranteed fix or timeline). Fail if it is interchangeable assign-me or +1 boilerplate, or over-promises. | required |
| Repo conventions and disclosure | The repo-facts block's contribution policy (the AI-use policy), read against the claim comment and repro report. Treat every package as AI-assisted work. | Judge only the AI policy here: missing template fields (such as pasted version dumps) are covered by the Environment check and are not failed again in this check. Disclosure is required ONLY if the policy text explicitly requires disclosing, declaring, or stating AI use; then the comments must contain that disclosure. A policy that only welcomes AI, or only says the contributor must understand and take responsibility for the work, requires nothing visible: pass. A policy that requires comments to be human-written in the contributor's own words is met by a comment that reads as specific, first-person work on this issue (not boilerplate); it needs no disclosure line. Fail only if a stated requirement is unmet. | required |
| Next step concrete | The end of the repro report | States a specific next step (what the author will try or fix next, or what a maintainer could check). | preferred |

## Verdict rule

Accept if every `required` check passes. Reject if any `required` check
fails. `unclear` on a `required` check counts as fail: proof that cannot
be verified is not ready to post. `preferred` checks never change the
verdict. (In a claim-only draft, leave out the checks that need the
repro report, per the skill.)
