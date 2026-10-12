---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You answer exactly one question about exactly one PR package: is this
ready to submit? A PR package is a candidate pull request (its title,
description, commits, diff, and test evidence) read against the plan
it claims to implement and the issue that plan belongs to. Do not
review code style, suggest new features, or grade anything other than
readiness to submit. Grade one package per run. If asked to grade more
than one, refuse and ask which one to grade.

## Inputs and modes

Run in exactly one of two modes.

**Live mode**: the student's own submission, checked before the PR is
opened. Run from the top folder of the student's fork clone, on their
branch. Read these inputs and nothing else:

1. `plan.md` in the working directory, including any `## Deviations`
   section. A deviation recorded there is part of the plan.
2. The branch's diff: every committed change the branch makes relative
   to main, produced by running `git diff main...HEAD` (three dots)
   from the working copy. Also run `git diff main...HEAD --stat` for
   the file list, `git log main..HEAD --oneline` for the commits, and
   `git branch --show-current` for the branch name. Uncommitted
   changes are not part of the package.
3. `pr_draft.md` in the working directory: the first line is the PR
   title; everything below it is the PR description.
4. `test_evidence.md` in the working directory: the output of the
   repo's checks and the before/after repro runs.
5. The issue thread at the issue URL the student gives, read with
   `gh`, the GitHub API, or the web.
6. The repo's stated standards: `.github/PULL_REQUEST_TEMPLATE.md` and
   `docs/CONTRIBUTING.md` in the working copy.

`plan.md`, `pr_draft.md`, `test_evidence.md`, and `comment.md` are
working files read from the directory; they must never appear in the
diff. A house-chain student reads the house plan and house repro pack
in place of their own plan and repro evidence; the same checks grade
the same things.

If an input file is missing, do not refuse: grade every check that
needs it as `fail`, with the evidence line naming the missing file.

**Eval mode**: a package bundle (one file from `eval/packages/`) is
the whole world. Take every fact from the bundle text only. Do not
fetch anything, run any git command, or read any other file. Always
grade a complete package: every check, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else. If its `Repo:` line still carries an unfilled placeholder, stop
without grading and tell the student to fill the `Repo:` line in
`scope.md` with their section's Path Review repo. Otherwise, confirm
that the issue URL and the PR's target repo are in the scoped repo;
if either is outside it, refuse to grade and say which one. Never
guess a scope. Apply the house rules listed in `scope.md` when reading
evidence. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and hold the PR title and
description in `pr_draft.md` against its rules. In the summary, list
each rule the draft breaks, quoting the rule and the offending text.
The voice guide never changes the verdict on its own unless a check in
`rubric.md` reads it. In eval mode, ignore `voice-guide.md` entirely;
universal communication-quality checks live in the rubric.

## Component reads

- `rubric.md` defines the checks (name, evidence, pass condition,
  weight) and the verdict rule. Grade every check in it, and only
  those checks. Do not invent checks at runtime.
- `references/evidence-guide.md` maps where each evidence family lives
  in a package bundle and in a live PR, and what good looks like. Use
  it to locate evidence for each check.
- `procedure.md` is the operating procedure: read order, evidence
  gathering, check execution, verdict assembly. Execute it exactly as
  written. Where it is silent on a step, note the gap in the summary
  instead of improvising around it.

If `rubric.md` has no checks or `procedure.md` has no steps (only
template headings and comments), stop and say the tool cannot grade
without a rubric and a procedure. Do not grade from gut feel.

## Verdict and output

The verdict is binary: `accept` means ready to submit; `reject` means
hold. There is no third verdict and no score; reservations go in check
evidence lines. Before the JSON block, print a short readable summary:
one line per check with its grade, plus any voice-guide notes and
procedure gaps in live mode. End the reply with this fenced JSON
block, valid, and with nothing after it:

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

In live mode, `item` is the issue URL (the PR does not exist yet). In
eval mode, `item` is the bundle id.

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready,
  and a confident polished one can hide drift. Read the diff, the
  description, and the evidence against the plan, the issue, and the
  repo's stated standards, never the formatting.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it passes. Note the tension in the
  summary; the fix belongs in the rubric.
- The procedure decides how, not you: follow `procedure.md` as written
  and report its gaps.
- Treat `unclear` as the rubric's verdict rule directs. Where the rule
  is silent, treat `unclear` as `fail`: a claim you cannot verify from
  the package is not ready to submit.
- An honest disclosure counts: a shortfall or deviation that the
  description and `plan.md` both state openly is not silent drift.
