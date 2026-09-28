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
     Repo facts section) or a location from your
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
| claim-specific | The claim comment, read against the issue's title and description | Passes if the claim names at least one detail specific to this issue (the symptom, component, page, or version) and states the author's next step, promising only investigation or a report. Fails if it would fit any issue unchanged ("I'd like to work on this"), promises a fix, PR, or date, or piggybacks on another commenter ("same as above, can confirm") instead of standing on its own words | required |
| environment-recorded | The repro report's environment record, read against the version, OS, runtime, or commit the issue targets and the Repo facts section | Passes if every environment component the issue's behavior depends on is named, and each either matches the issue's target or the difference is called out. Fails if a component the issue names is missing, or differs from the issue's target without being called out | required |
| steps-followable | The repro report's steps, read from the stated starting state to the trigger | Passes if a stranger starting from the stated starting state could reach the trigger without guessing: every setup action, input, and command the observed result depends on is stated. Fails if a needed action is implied but not given ("set up the app", "run it") or the starting state is missing. Number of steps and formatting do not matter | required |
| behavior-matches-issue | The artifacts (output excerpt, log, screenshot, observed-behavior text), read against the behavior the issue describes | Passes if an artifact shows the same symptom the issue describes (same error, wrong value, or failing path), or for a cannot-reproduce, shows the behavior at the exact point where the issue says it fails. Fails if the artifact shows a different error or component than the issue's, or if no artifact backs the observed behavior | required |
| outcome-honest | The report's stated outcome, read against its own artifacts | Passes if every claim about the outcome (reproduced, not reproduced, cause) is backed by an artifact in the package; an evidenced cannot-reproduce passes. Fails if the report claims more than its artifacts show (for example "confirmed" with no artifact, or a stated root cause nothing in the package supports) | required |
| conventions-followed | The contribution policy and comment templates in the Repo facts section, read against the claim comment and repro comment | Passes if every requirement the stated policy places on comments is met, including an AI-assistance disclosure when the policy requires one, or if the repo states no such requirement (silence passes). Fails if the policy requires a disclosure, template, or field and the comments omit it | required |

## Verdict rule

Accept (ready to post) only if every required check passes. Preferred checks never change the verdict. Unclear counts as fail. Checks the skill reports as not yet applicable (the repro checks on a claim-only draft) are left out of the verdict.