# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis_fits_evidence | The plan's stated cause read against what the repro evidence shows | The stated cause explains the reproduced behavior and contradicts nothing in the repro evidence | required |
| targets_cause | The plan's approach and files to touch read against where the repro evidence locates the cause | The change acts on the cause the evidence points to, not only on where the symptom appears | required |
| bounded_change | The plan's scope statement read against the issue | It is one bounded change that fixes this issue, and nothing in it is unrelated to the issue | required |
| stranger_can_start | The plan's change: the files, function or area, and approach it names | A stranger could begin the work without asking the author a question: the plan says where the change goes and what the change is, or names the concrete step that will pin down any detail still open | required |
| test_proves_fix | The test plan read against the repro evidence's steps | Re-running it gives an observable result that would differ if the fix did not work | required |
| unknowns_stated | The plan's risks and unknowns read against the claims its change depends on | No claim the change depends on is presented as certain when the repro evidence does not support it, and open questions the plan has are named | required |
| thread_and_conventions | The plan comment read against the thread highlights and the repo-facts block | The comment does what the thread asks of it (does not ignore or contradict it) and follows the repo's stated conventions | required |

## Verdict rule

Accept if every required check passes. Preferred checks never change the verdict. Unclear counts as fail.
