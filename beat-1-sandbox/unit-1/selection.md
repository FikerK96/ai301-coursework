# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12

**Verdict output**

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Ranked read-out

  1. #12 — Add snapshot tests for prompt templates — ACCEPT
  Best fit. It's a pure test-writing task, which is the thing you named most specifically for AI 301. tests/unit/test_prompt_templates.py already
  exists on main, so you're extending a file rather than bootstrapping one, and the deliverable is well-defined: snapshot tests that fail when a
  template changes without a version bump. Python, 3–5 hours.

  2. #18 — Repo analyzer never receives a file list, so has_tests and has_ci are always False — ACCEPT
  Your feature-implementation slot, and it carries the tests label too, so it's double-value. You'd make GitHubTool fetch a file list and populate
  file_structure so _detect_tests() / _detect_ci() stop returning False. Two source files, 2–4 hours. Heads up: there's no
  tests/unit/test_repo_analyzer.py on main, so the test side means writing a new file, not editing one.

  3. #47 — API docs don't include example curl commands — ACCEPT
  Your documentation slot. Single file (docs/API.md), add example invocations per endpoint, 2–3 hours. Lowest ceiling of the three for learning, but
  the cleanest first PR if you want to get the workflow itself under your belt before the heavier work.

  Taken together these three cover all three things your fit profile asked for — tests (#12), feature implementation (#18), documentation (#47) —
  which the previous batch (#63/#64/#73) did not, since that set had no feature work.

  One carry-over from docs/CONTRIBUTING.md: seeded bugs carry @pytest.mark.xfail(strict=True) markers that must be removed as part of the fix, or CI
  fails. #18 describes bug-shaped behavior despite its enhancement label — grep for an xfail naming issue #18 before you open the PR.

  Per-check grades (identical across all three):

  ┌──────────────────────────────┬──────┬──────┬──────┐
  │            Check             │ #12  │ #18  │ #47  │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ Repo not archived            │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ Repo in use                  │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ Maintainer commits           │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ Maintainer responds          │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ Bounded scope                │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ Legitimate request           │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ No assignee                  │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ No active PR                 │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ No live claim                │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ No AI ban                    │ pass │ pass │ pass │
  ├──────────────────────────────┼──────┼──────┼──────┤
  │ Friendly signals (preferred) │ pass │ pass │ pass │
  └──────────────────────────────┴──────┴──────┴──────┘

  [
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12",
      "checks": [
        {"name": "Repo not archived", "grade": "pass", "evidence": "Repo API: archived: False"},
        {"name": "Repo in use", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:50:20Z, 5 days before capture date 2026-09-21 (no releases 
  exist)"},
        {"name": "Maintainer commits", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 by Aburke225 (Andrew Burke), a person, 
  within 90 days"},
        {"name": "Maintainer responds", "grade": "pass", "evidence": "Oldest issue in repo created 2026-09-10, 11 days before capture; all sampled 
  issues set aside as <14 days old, so rubric says pass"},
        {"name": "Bounded scope", "grade": "pass", "evidence": "One deliverable: 'Add snapshot tests that fail if a template's content changes 
  without a version bump', relevant file tests/unit/test_prompt_templates.py; no umbrella/tracking language, not a usage question, 0 comments so no 
  unsettled debate"},
        {"name": "Legitimate request", "grade": "pass", "evidence": "Author Aburke225, author_association COLLABORATOR, labels ['enhancement','good 
  first issue','devops','rag','tests','tier-1']"},
        {"name": "No assignee", "grade": "pass", "evidence": "assignees: NONE"},
        {"name": "No active PR", "grade": "pass", "evidence": "Repo has 0 pull requests total (state=all); timeline shows only 6 'labeled' events, no
  cross-references; 0 comments"},
        {"name": "No live claim", "grade": "pass", "evidence": "comments: 0 — no claim comments exist"},
        {"name": "No AI ban", "grade": "pass", "evidence": "docs/CONTRIBUTING.md, PR template and README contain no mention of AI-generated 
  contributions; silence passes"},
        {"name": "Friendly signals", "grade": "pass", "evidence": "Has 'good first issue' label AND opened by COLLABORATOR Aburke225"}
      ],
      "verdict": "accept"
    },
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/18",
      "checks": [
        {"name": "Repo not archived", "grade": "pass", "evidence": "Repo API: archived: False"},
        {"name": "Repo in use", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:50:20Z, 5 days before capture date 2026-09-21 (no releases 
  exist)"},
        {"name": "Maintainer commits", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 by Aburke225 (Andrew Burke), a person, 
  within 90 days"},
        {"name": "Maintainer responds", "grade": "pass", "evidence": "Oldest issue in repo created 2026-09-10, 11 days before capture; all sampled 
  issues set aside as <14 days old, so rubric says pass"},
        {"name": "Bounded scope", "grade": "pass", "evidence": "One deliverable across two named files (agent/tools/github_tool.py, 
  ingestion/parsers/repo_analyzer.py): supply a file list under 'file_structure'; maintainer estimate 2-4 hours; no umbrella language and no 
  maintainer statement that it needs core-internals changes"},
        {"name": "Legitimate request", "grade": "pass", "evidence": "Author Aburke225, author_association COLLABORATOR, labels ['enhancement','good 
  first issue','agent','tests','tier-1']"},
        {"name": "No assignee", "grade": "pass", "evidence": "assignees: NONE"},
        {"name": "No active PR", "grade": "pass", "evidence": "Repo has 0 pull requests total (state=all); timeline is 5 'labeled' events plus a 
  'renamed' event by maintainer Aburke225 on 2026-09-16, no cross-references; 0 comments"},
        {"name": "No live claim", "grade": "pass", "evidence": "comments: 0 — the only post-creation timeline event is a maintainer rename, not a 
  claim"},
        {"name": "No AI ban", "grade": "pass", "evidence": "docs/CONTRIBUTING.md, PR template and README contain no mention of AI-generated 
  contributions; silence passes"},
        {"name": "Friendly signals", "grade": "pass", "evidence": "Has 'good first issue' label AND opened by COLLABORATOR Aburke225"}
      ],
      "verdict": "accept"
    },
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/47",
      "checks": [
        {"name": "Repo not archived", "grade": "pass", "evidence": "Repo API: archived: False"},
        {"name": "Repo in use", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:50:20Z, 5 days before capture date 2026-09-21 (no releases 
  exist)"},
        {"name": "Maintainer commits", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 by Aburke225 (Andrew Burke), a person, 
  within 90 days"},
        {"name": "Maintainer responds", "grade": "pass", "evidence": "Oldest issue in repo created 2026-09-10, 11 days before capture; all sampled 
  issues set aside as <14 days old, so rubric says pass"},
        {"name": "Bounded scope", "grade": "pass", "evidence": "One deliverable in one file: add example curl invocations to docs/API.md; maintainer 
  estimate 2-3 hours; not an umbrella, not a usage question, 0 comments so no unsettled debate"},
        {"name": "Legitimate request", "grade": "pass", "evidence": "Author Aburke225, author_association COLLABORATOR, labels ['good first 
  issue','docs','tier-1']"},
        {"name": "No assignee", "grade": "pass", "evidence": "assignees: NONE"},
        {"name": "No active PR", "grade": "pass", "evidence": "Repo has 0 pull requests total (state=all); timeline shows only 3 'labeled' events, no
  cross-references; 0 comments"},
        {"name": "No live claim", "grade": "pass", "evidence": "comments: 0 — no claim comments exist"},
        {"name": "No AI ban", "grade": "pass", "evidence": "docs/CONTRIBUTING.md, PR template and README contain no mention of AI-generated 
  contributions; silence passes"},
        {"name": "Friendly signals", "grade": "pass", "evidence": "Has 'good first issue' label AND opened by COLLABORATOR Aburke225"}
      ],
      "verdict": "accept"
    }
  ]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

RUN 1 (partial run on issue 1-3)
Date: Sep 20
Rubric change (what and why): first draft, 9 required checks + 1 preferred
Score: 2/3
Disagreements (issue ids): issue-01 (gold accept, mine reject)
Notes on each disagreement: Maintainer responds, Bounded scope
Change for run 2: 14-day exclusion + 45-day response window; narrowed the umbrella definition

RUN 2 (partial run on issue 1-3)
Date: Sept 20
Rubric change (what and why): Maintainer responds now ignores issues under 14 days old and allows 45 days; Bounded scope narrowed to explicit umbrella/split language
Score: 3/3
Disagreements: none
Notes: tuned on issue-01, so not proof the rubric generalizes

RUN 3 (full run)
Date: Sept 20 
Rubric change: none since run 2 
Score: 18/20 (PASS) 
Disagreements: issue 14 (gold accept, mine reject. Failed Maintainer responds), issue 20 (gold reject, mine accept, no check failed)

RUN 4 (partial: only issue 14,issue 01) 
Date: Sept 20 
Rubric change: Maintainer responds now passes when no sampled issue is 14+ days old (nothing to judge). 45-day rule still applies when one is 
Cause: issue-14's sample was a single 1-day-old issue, so the check had no evidence and unclear counted as fail 
Score: 2/2 
Disagreements: none

RUN 5 (partial: only issue 20,issue 14,issue 01)
Date: Sept 20
Rubric change: added Legitimate request check 
Cause: issue-20 (gold reject) passed every check
Score: 3/3
Disagreements: none

LIVE RUNS 
Date: Sept 21
Batch 1: #63, #64, #73: all accept, ranked #63 > #64 > #73 
Batch 2: #12, #18, #47: all accept, ranked #12 > #18 > #47 
Chosen: 12
Reason: pure test writing in python is something I was looking forward to going over, and it was one of the issues ranked first between the 2 batches fitting my profile

**Issue analysis**

issue-20 

Gold label: reject.

My rubric's decision: in run 3 it graded accept, with no failed check: "issue-20  reject  accept   NO     graded accept". After I fixed it, the final full run graded reject: "issue-20  reject  reject   yes".

Why my rubric first accepted it: the repo was healthy (a push and commits the day before capture, and a sampled issue answered in "0.1 days"), the request was one bounded feature, nothing was assigned or claimed, and the bundle has "(no comments)". Every check I had passed. None of them asked whether the issue itself was legitimate. The bundle shows it was "opened by cursor[bot] (NONE) on 2026-08-02, state open, labels: none", with no comments, and its own text says "Logo asset TBD." Nobody with standing in the repo had looked at it, so a newcomer would be claiming a ticket no maintainer had asked for.

What I changed: I added the Legitimate request check, which fails an issue opened by a bot account with no Owner, Member or Collaborator reply, and an issue with no labels, no comments and association NONE. Run 5 (--only issue-20,issue-14,issue-01) then gave "agreement: 3/3 scored items", so issue-20 flipped to reject while issue-14 and issue-01 stayed accept.

**Check rationale**

The check I picked is Legitimate request. This is how it's written in the rubric.md I uploaded:

| Legitimate request | Issue author, author association, and labels in the Issue header, plus the Comments section | Fails if the author is a bot account (name ending in [bot]) and no Owner, Member or Collaborator has commented in the thread. Also fails if the issue has no labels, no comments, and the author association is NONE, meaning nobody with standing has looked at it. Otherwise passes | required |

I wrote this one after issue-20 got through my rubric even though gold said reject. Every other check passed on it, because the repo was healthy and the request was small, so I needed something that looked at the issue itself. I pointed the evidence at the author, the author association, the labels and the comments because those are always in the bundle, so anyone grading it would find the same things.

I split the pass condition in two. The bot part is there because a bot-opened issue that no maintainer has answered has no real person behind it. The second part needs all three signals at once (no labels, no comments and association NONE), because plenty of good issues have no comments, and issue-01 is one of them. I only wanted to fail an issue when nobody with standing had touched it at all. I made it required because I wouldn't want a newcomer spending a first PR on a ticket the maintainers never asked for.

**Trade-offs**

The main thing this check gives up is brand-new issues from outside contributors. If someone opens a real bug report an hour ago, it has no labels and no reply yet, so it looks the same as an abandoned or auto-generated ticket and my rubric would reject it. I'm okay with that miss, since a first issue that no maintainer has looked at is a risky one to claim anyway.

To check that adding it didn't break anything, I re-ran "--only issue-20,issue-14,issue-01" and got "agreement: 3/3 scored items". issue-20 flipped to reject, and issue-14 and issue-01 stayed accept, since both were opened by human contributors and have labels. Then the final full run gave "agreement: 20/20 scored items  (bar: 18/20: PASS)", so it didn't wrongly reject any of the accept-gold issues. In live mode, #12, #18 and #47 also passed it, since each was opened by a COLLABORATOR and has labels.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.

I picked #12 -> Add snapshot tests for prompt templates

2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
   
it has passed every required check. The repo is active, nobody is assigned, there are no comments or linked PRs, and a collaborator opened it with the good first issue label.

3. The anticipated difficulty in claiming it.]

It's the longest of the three, and I may need to learn how snapshot tests work.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
