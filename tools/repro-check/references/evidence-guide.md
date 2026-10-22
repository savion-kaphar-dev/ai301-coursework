# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives:
- Eval bundle: the first lines of the "Candidate repro report" (an "Environment:" line or similar). The issue's target environment is in the "Issue" section (body, "Environment:" line) and the "Thread highlights". The "Repo facts" block says what the bug-report template asks for.
- Live: the repro draft's environment line; the issue body and thread for the target; the repo's issue template.

What good looks like: the report names OS, the tool's version, and anything the behavior depends on (shell, driver, build profile, runtime) that the issue's behavior plausibly turns on. Where it differs from the issue's target, the report says so (for example "issue filed on 0.63.1, I ran 0.64.1"). A missing record, or a silent deviation (an older version, a different OS on an OS-specific issue), is a fail.

## Steps

Where it lives:
- Eval bundle: the commands and numbered steps in the "Candidate repro report". Compare them against the steps and trigger in the "Issue" section.
- Live: the repro draft's commands, read as if you had only the draft.

What good looks like: starting from a clean machine, a stranger can run each step in order and reach the trigger the issue names. The trigger itself must be present and unchanged (the same syntax, flags, input, config). Inputs are inline or public. Fail on a skipped or altered trigger, or on a step that needs a private repo, an unshared config, or an unstated setting.

## Behavior shown

Where it lives:
- Eval bundle: the output excerpts, logs, exit codes, and transcripts in the "Candidate repro report", read against the symptom described in the "Issue" body (the exact error text, panic, exit code, or visible effect).
- Live: the pasted output or screenshots in the draft, against the issue's description.

What good looks like: the artifact is the issue's symptom, not a neighbor. Compare the specifics: the same error message or exit code, produced with the issue's input. Adjacent behaviors to reject: a graceful validation error where the issue reports a crash, a syntax error from an input the author modified, an old version's different error, garbled output where the issue reports a crash, or a transcript that only shows the tool starting. A control run (changing one thing and seeing the symptom go away) strengthens it. Ignore formatting and length; judge only the artifact.

## Honesty

Where it lives:
- Eval bundle: the conclusion sentences in the "Candidate repro report" ("confirmed", "reproduced", "root cause is...", "also affects...") and the assertions in the "Candidate claim comment", each read against the artifacts in the report.
- Live: the same sentences in the drafts.

What good looks like: every claim has a shown artifact behind it. "I verified" with no transcript, a root-cause diagnosis with no evidence, certainty or generalization (other platforms, other releases) beyond what was run, and a narration that misdescribes the artifact are all fails. A report that says "could not reproduce" and shows the real attempt, with what differed from the issue's setup, is a pass: an honest negative is ready to post.

## Comms

Where it lives:
- Eval bundle: the "Candidate claim comment" and the report's prose, read against the "Issue" section, and against the "Repo facts" block's bug-report template asks and contribution policy (including any AI-use policy).
- Live: the draft comments, the repo's issue template, CONTRIBUTING.md, and any AI policy file.

What good looks like: 
- The claim is specific: it names what this author will do on this issue, tied to the issue's content, and promises no guaranteed fix or timeline. Interchangeable "assign me" or "+1" text is a fail.
- The comments supply what the template asks for.
- Disclosure is required only when the repo-facts policy text explicitly says to disclose, declare, or state AI use (look for those verbs). Then the comments must contain it. Treat every package as AI-assisted when applying this.
- A policy that only welcomes AI, or only asks the contributor to understand and take responsibility, imposes nothing visible: no disclosure needed, and none is penalized.
- A policy that says comments must be human-written in the contributor's own words is met by first-person, issue-specific comments; it does not call for a disclosure line.
