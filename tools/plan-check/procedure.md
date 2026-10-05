# Procedure: how this skill grades a plan package

## Read order

1. Read the repro evidence first. For each step, note what condition it changed and its result.
2. Read the issue. Note the reported behavior in one sentence.
3. Read the thread. Note maintainer directions, open questions, and causes already identified.
4. Read the repo facts. Note the file paths that exist and every policy requirement or convention stated.
5. Read the plan.
6. Read the plan comment last.
7. Reading the evidence before the plan stops the plan's confident story from shaping how it is read.

## Evidence gathering

For each check, record the plan text it depends on (quoted) next to the evidence it is compared with (quoted). If the plan says nothing relevant, record "absent."

1. diagnosis_fits_evidence: record the plan's stated cause. Compare it with the repro evidence's steps and results, the original issue, and causes identified in the thread.
2. targets_cause: record the plan's approach and files to touch. Compare them with where the repro evidence locates the cause.
3. bounded_change: record the plan's scope statement. Compare it with the issue's reported behavior.
4. stranger_can_start: record the plan's approach and files to touch. Note whether they say where the change goes and what the change is, and, for any detail left open, the step the plan gives to pin it down.
5. test_proves_fix: record the plan's test plan. Compare it with the repro evidence's steps and results.
6. unknowns_stated: record the plan's risks and unknowns. Compare them with any claim elsewhere in the plan that the repro evidence does not establish.
7. thread_and_conventions: record the plan comment. Compare it with the maintainer directions from the thread and the policy requirements from the repo facts.

## Check execution

1. Run the checks in the order they appear in the rubric table.
2. Grade each check P, F, or ? by applying its pass condition to the quotes recorded for it.
3. If adequate evidence for a required check is missing (recorded as "absent"), the check cannot pass: grade it F.
4. Exception for unknowns_stated: if the plan states no risks or unknowns, grade it P when no claim its change depends on goes beyond what the repro evidence supports, and F otherwise.
5. Grade ? only when the evidence is present but supports both P and F.
6. diagnosis_fits_evidence: the plan's identified cause must not conflict with the repro evidence or the issue thread, and must align with causes already identified there.
7. Grade from the recorded quotes. Re-read the package only if the quotes are not enough to apply the pass condition.
8. Grade every check, even after one fails.

## Verdict assembly

1. Ready (accept) only if all required checks affirmatively pass.
2. A ? is not an affirmative pass, so it counts as a fail.
3. Preferred checks never change the verdict.
4. If the verdict is hold (reject), quote the first required check in table order that did not pass, with its recorded plan text (or "absent") and the evidence it was compared with.
