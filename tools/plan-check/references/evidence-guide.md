# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives:
- Eval package: the `Cause:` line of the Candidate plan, read against the Repro evidence's Steps, Expected, and Actual, and against the Issue body.
- Live: the Diagnosis section of the draft plan.md, read against the student's posted repro comment and the issue thread.

What good looks like: the stated cause explains every result the repro evidence shows, including steps where a condition changed, and contradicts none of them. In calib-01, the cause ("the view's model is not refreshed after a push") explains both step 3 (color stays stale) and step 4 (re-entry fixes it).

## Scope

Where it lives:
- Eval package: the `Change:` paragraph of the Candidate plan, especially its `In:` and `Out:` lines, read against the Issue.
- Live: the Scope section of the draft plan.md, read against the issue.

What good looks like: one change aimed at the reported behavior, with anything nearby that could tempt a rewrite explicitly left out. In calib-01, `In:` is one callback in one file, and `Out:` excludes how push status is computed and other views' refresh behavior.

## Executability

Where it lives:
- Eval package: the `Change:` paragraph of the Candidate plan (files, function or area, approach).
- Live: the Files and Approach sections of the draft plan.md, read against the fork's actual file tree.

What good looks like: a stranger could open the named file and make the first edit without asking the author anything. In calib-01, the plan names `pkg/gui/controllers/sync_controller.go`, the push completion callback, and the exact change (add the commits context to its post-push refresh scope). A detail left open still passes when the plan names the concrete step that will pin it down (pkg-14: exact functions pinned by tracing with `zellij --debug`).

## Test plan

Where it lives:
- Eval package: the `Test:` line of the Candidate plan, read against the Repro evidence's numbered Steps and Expected.
- Live: the Test plan section of the draft plan.md, read against the repro steps in the student's posted repro comment.

What good looks like: it re-runs the repro steps and names an observable result at a specific step that would be different if the fix failed. In calib-01: "at step 3 the color must flip without leaving the view." A test that only passes or fails on a crash, or that can't show the reported behavior changed, is not decisive.

## Honesty

Where it lives:
- Eval package: any risks or unknowns the Candidate plan states, plus every claim in `Cause:`, `Change:`, and `Test:` that the Repro evidence does not establish.
- Live: the Risks and unknowns section of the draft plan.md, and the Deviations section after the build (where an honest mid-build change gets recorded).

What good looks like: any claim the repro evidence doesn't establish is stated as uncertain, or is turned into something the test plan checks. A plan with no risks section can still pass if it asserts nothing beyond the evidence. In calib-01, the claim that force push "shares the callback" isn't shown by the repro, but the test plan checks it directly.

## Comms

Where it lives:
- Eval package: the Candidate plan comment, read against the Thread highlights and the Repo facts (bug-report template, contribution policy, and any AI-disclosure requirement).
- Live: the draft comment.md, read against the issue's GitHub thread and the repo's CONTRIBUTING.md, issue templates, and contribution policy.

What good looks like: the comment responds to what the thread and the repo actually ask, rather than reading as boilerplate that could be posted on any issue. In calib-01 the thread is empty, and the comment points to the reproduction and says it will keep the PR minimal "given the review-bandwidth note in CONTRIBUTING," which addresses the repo's stated policy.
