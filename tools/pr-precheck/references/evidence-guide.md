# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Rubric checks: diff_within_plan, plan_delivered, description_matches_diff, claims_backed_by_diff.

Where it lives:
- Eval package: Plan context (the `Plan:` steps, `Not in scope:`, and `Files:` lines), read against the Candidate PR's Diff (the `--- a/` and `+++ b/` file headers and each hunk). The Title and Description (including any checklist) are read against the same Diff.
- Live: `plan.md` (its files, steps, out-of-scope items, and `## Deviations`), read against `git diff main...HEAD` and `git diff main...HEAD --stat`. The title (line 1 of `pr_draft.md`) and the description (its Summary, Changes, and Testing checkboxes) are read against the same diff.

What good looks like: every file in the diff is named in the plan's `Files:` (the file or its folder) or recorded in Deviations with a reason; every plan step has a hunk that carries it out or a stated reason it was left out; every change and every item marked done in the description has a matching hunk or file in the diff, and every hunk is covered by the description. In calib-01, the plan names `themes.gitconfig`, the diff touches only that file and removes only the shadowed line, and the description claims exactly that.

Silent drift, both directions:
- More than the plan: calib-03 rewrites `src/language-js/print/property.js`, which the plan never names, while the description says "exactly, with no changes beyond it". calib-02 bumps tcell in `go.mod`/`go.sum` and edits `pkg/gui/gui.go`, none of which the plan names.
- Less than the plan: calib-02 never touches the gocui Windows input translation the plan names. calib-03's checklist claims fixtures for the all-comments control and nested chains, but the diff adds only `blank-line-before-else.js`.
- An honest disclosure re-ties a mismatch: a gap or extra change stated in the description or in Deviations with its reason is not drift.

## Test evidence (harness category: not-tested)

Rubric checks: evidence_observable, repo_checks_run.

Where it lives:
- Eval package: the Candidate PR's Test evidence section, read against the `Test plan:` in Plan context, with Plan context's `Repro evidence` as the before. Suites or checks the repo asks for are in Repo facts; their results may also be stated in the Description.
- Live: `test_evidence.md` (the before and after repro runs and the output of `make test-unit`, `make test-integration`, `make lint`, and `make typecheck`), read against the Test plan in `plan.md`. The checks to run are listed in `.github/PULL_REQUEST_TEMPLATE.md`; the description's Testing section must report the same results.

What good looks like: the issue's repro is re-run on the change, and the after is a concrete observation that differs from the before as the test plan predicts. It may be printed output (pkg-05's table now shows both `atuin` rows) or a specific observation in a note (pkg-11: "after: searches normally, no error"; pkg-13: the browser shows the full URL and `:wait()` returns code 0). Every other failure mode the test plan names as proof gets its observed result, or a stated reason it was left out. Every suite or check the plan or repo names is reported with its outcome, printed or stated specifically (pkg-11: "`cargo test -p ignore` passes (214 tests)"; pkg-05: "fmt and clippy clean"). A failing or empty result (Path Review's `make test-integration` prints "no tests ran") is good evidence when reported honestly. Controls and smoke checks may be stated briefly.

What it is not: no evidence at all (calib-02: "(none provided)"), or an admission the fix was never run on the reported case (calib-02: "did not get a chance to test"); an after that is only a verdict with no observation ("works", "fixed", "should be fine"); a failure mode the test plan names left out silently (calib-04 shows repro 1 but never repro 2, `-j 200000 -x echo .`); a suite the plan or repo names that is never mentioned, or mentioned only vaguely ("ran the tests").

## Diff quality (harness category: unreviewable)

Rubric check: no_debris.

Where it lives:
- Eval package: every hunk of the Candidate PR's Diff, and the Commits list (commit messages like "gofmt" or "cleanup" point to churn).
- Live: every hunk of `git diff main...HEAD`, and `git log main..HEAD --oneline`. `git diff main...HEAD --stat` must list only files the fix changes; `plan.md`, `pr_draft.md`, `test_evidence.md`, and `comment.md` must never appear.

What good looks like: every added or removed line is part of the fix, its test, or an asked-for artifact such as a changelog entry, so a reviewer sees the change and nothing else. In calib-04, the diff is the parser, its test, and the CHANGELOG line, with nothing riding along.

Debris tells: debug output (`print`, `console.log`, `dbg!`) left in; commented-out code; whitespace-only or formatting-only edits to lines the fix does not need (calib-02's gofmt commit rewrites unrelated assignments in `pkg/gui/gui.go`); drive-by refactors (calib-03's `property.js` rewrite); unrelated dependency bumps (calib-02's tcell bump); working files committed by mistake.

## Standards and comms (harness category: standards-wall)

Rubric checks: standards_asks_met, ai_disclosure, branch_name.

Where it lives:
- Eval package: the `pull requests:` line of Repo facts (the template's sections and checklist, and the issue-reference ask) and the `contribution policy` line (any AI policy), read against the Candidate PR's Title, Description, and Commits. The branch name appears only if the package shows one.
- Live: `.github/PULL_REQUEST_TEMPLATE.md` (Summary, Issue, Changes, Testing, Screenshots / Demo, Notes for Reviewers) and `docs/CONTRIBUTING.md`, read against `pr_draft.md`. The AI-use disclosure, which the course always requires, goes in Notes for Reviewers. The branch name comes from `git branch --show-current`.

What good looks like: every section and checklist item the repo asks for is present and filled with content true of this PR (N/A with a reason counts), the issue is referenced in the form the repo asks for (live: `Closes #N`), and where an AI policy applies, the description says in the author's own words how AI was used. If the repo states no template and no AI policy, referencing the issue is enough: calib-01's description references #2211 and passes.

What it is not: a template's sections or checklist ignored (calib-02's description skips lazygit's requirements checklist entirely); boilerplate that could sit on any PR; a required disclosure missing; a branch with no type prefix or issue number (preferred, never changes the verdict).
