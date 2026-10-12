# Procedure: how this tool grades a PR package

## Read order

Where each part lives: in eval mode, the named sections of the bundle; in live mode, the source given in brackets.

1. Live mode only: read `scope.md` first and apply the scope seam in SKILL.md before reading anything else.
2. Read Plan context [live: `plan.md`, including `## Deviations`]. List: the repro evidence's before results, every file and folder the plan names, every step it commits to, every Not-in-scope item, every deviation, and every item in the Test plan, marking each as either proof of the fix (a repro or named failure mode) or a control, smoke check, or test suite.
3. Read the Issue and Thread highlights [live: the issue thread at the given URL]. Note the reported behavior in one sentence and any maintainer direction.
4. Read Repo facts [live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`]. List every PR ask: template sections, the required issue-reference form, every check the repo says to run, and any AI policy. Live mode also adds the course rule that every PR discloses AI use. If the repo states none of these, write "none stated" for each.
5. Read the Diff [live: `git diff main...HEAD`, plus `git diff main...HEAD --stat` for the file list]. List every changed file and, per file, each hunk in one line.
6. Read the Commits [live: `git log main..HEAD --oneline`] and the branch name if shown [live: `git branch --show-current`].
7. Read the Test evidence [live: `test_evidence.md`]. List each command shown and whether printed output follows it.
8. Read the Title and Description last [live: line 1 of `pr_draft.md` is the title, the rest is the description]. List every claim: each change claimed, each fidelity claim ("exactly", "no changes beyond", "nothing added"), each item marked done, each test result stated, each disclosure of a shortfall or deviation, and the AI-use statement.
9. Why this order: the plan sets the standard, the diff and evidence are what was actually done, and the description is what the author says was done. Reading the description last stops its confident claims from shaping how the diff and evidence are read.

## Evidence gathering

For each check, record the side being checked (quoted) next to what it is compared with (quoted). If a side has nothing relevant, record "absent". Record any disclosure from the Description or Deviations that bears on the check.

1. diff_within_plan: record each changed file from the diff next to the plan's named files and folders, its Not-in-scope items, and its deviations. Mark each file as named, disclosed with a reason, or outside both.
2. plan_delivered: record each step the plan commits to next to the hunk in the diff that carries it out, or "absent", plus any disclosure that it was left out.
3. description_matches_diff: record each change and fidelity claim in the Title and Description next to the diff hunk that confirms or contradicts it. Then record each diff hunk the description does not cover.
4. claims_backed_by_diff: record each item marked done (tests, changelog, docs) next to the matching file or line in the diff, or "absent".
5. evidence_observable: record the issue's repro and each other Test-plan item marked as proof of the fix, next to its command or steps and the observed after result in Test evidence (printed output or a specific observation), and the before (from Test evidence or Plan context's repro evidence). Mark each after as an observation or a bare verdict ("works", "fixed"). Record "absent" for any item not reported, plus any disclosure that it was not run.
6. repo_checks_run: record each test suite the Test plan names and each check the repo lists, next to its reported outcome in Test evidence or the Description (printed or stated specifically), or "absent". Record "none named" if neither names any.
7. no_debris: record every hunk that adds debug output, adds commented-out code, only reformats or changes whitespace on lines the fix does not need, or edits code unrelated to the issue.
8. standards_asks_met: record each PR ask from Repo facts next to the Description text that meets it, or "absent". Record the issue reference as written.
9. ai_disclosure: record the AI policy that applies (or "none stated" in eval mode when Repo facts states none) next to the Description's AI-use statement, or "absent".
10. branch_name: record the branch name, or "not shown".

## Check execution

1. Run the checks in rubric table order.
2. Grade each check P, F, or ? by applying its pass condition to the quotes recorded for it.
3. If evidence a required check needs is recorded "absent" and no disclosure covers it, grade F.
4. If a disclosure in the Description or Deviations openly states the shortfall or deviation the check would catch, grade the disclosure as the evidence and grade P. A disclosed change unrelated to the issue still fails no_debris.
5. Conditional passes: repo_checks_run is P when "none named"; standards_asks_met is P when the repo states no asks beyond referencing the issue and the issue is referenced; ai_disclosure is P when no AI policy applies; branch_name is P when "not shown".
6. Grade ? only when the evidence is present but supports both P and F.
7. Grade from the recorded quotes. Re-read a part of the package only if the quotes are not enough to apply the pass condition.
8. Grade every check, even after one fails.
9. Live mode: after grading, check the Title and Description against `voice-guide.md` and list each broken rule in the summary. This never changes a grade.

## Verdict assembly

1. Accept only if every required check is P.
2. A ? is not P, so it counts as a fail.
3. Preferred checks (branch_name) never change the verdict.
4. If the verdict is reject, quote the first required check in rubric table order that is not P: its name, the recorded quote being checked (or "absent"), and what it was compared with. Put that in the summary, and in that check's JSON evidence line.
5. Map grades to the JSON: P is "pass", F is "fail", ? is "unclear". Write one JSON entry per rubric check, in table order, each with a one-line evidence string, then the verdict.
