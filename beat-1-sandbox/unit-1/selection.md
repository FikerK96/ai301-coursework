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

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
