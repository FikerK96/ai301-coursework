# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

FikerK96

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5863202023

I'm claiming this, and will set up the repo, edit one prompt template's content, run to check whether any test fails today. I'll post a repro report here with my environment with steps and the test output.


**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5863802231

**Outcome:** Reproduced. Changing a prompt template's content without bumping its version does not fail any test in `tests/unit/test_prompt_templates.py`.

### Environment
- macOS 26.5 (Apple Silicon), Python 3.12.13, pytest 9.1.1
- Commit `2f4e82f` on `main`, set up per docs/SETUP.md (`make setup` run with Python 3.12, since my system Python is 3.9)

### Steps
1. Run `.venv/bin/pytest tests/unit/test_prompt_templates.py -q`: 37 passed.
2. In `rag/generator/prompt_templates.py`, line 21 (`skills_feedback` `"v1"`), change `4. Framework and tool mastery` to `4. Framework and tool mastery (content changed, version still v1)`, leaving the `"v1"` key alone.
3. Re-run the same test file.

### Result
Template content changed with no version bump, and nothing failed:
```
.....................................                                    [100%]
37 passed in 0.09s
```
`test_template_snapshot_content_hash` computes a hash of the templates but only checks that it's a 32-character string. It never compares it to a saved value, so any content change passes:
```
assert isinstance(content_hash, str)
assert len(content_hash) == 32  # MD5 hash length
```
I reverted the edit afterward.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1: full run
"agreement: 20/20 scored items  (bar: 18/20: PASS)"
Date: Sep 27
Score: 20/20
Disagreement: NONE

Before doing second run evidence-guide.md Environment now counts bug-report template fields as required environment. rubric.md unchanged


Run 2: full run
"agreement: 18/20 scored items  (bar: 18/20: PASS)"
Date: Sep 27
Score: 18/20
Disagreement: pkg 03, pkg 09. 



**Package analysis**

pkg-03 (ripgrep #2779, wrong line numbers with multiline --replace).

Gold said accept. My rubric said reject in the saved run: "pkg-03  accept  reject   NO     failed: outcome-honest". It had graded accept in Run 1 with the same rubric.

Everything else passed. The repro shows the exact wrong output from the issue ("1:fnord 2:boccob 3:d321fdddffff 4:clowns"). It only failed outcome-honest, because the grader flagged: "Claims dropping `-r '$1'` \"reports 1, 4, 7, 10 correctly\" with no output block shown for that run."

That comes from my wording. The check "Passes if every claim about the outcome (reproduced, not reproduced, cause) is backed by an artifact in the package", and the report's last sentence makes an extra claim with no output shown for it. Read strictly, "every claim" catches it.

I think gold is right. The main result is fully backed by the output, and the extra sentence just repeats what the owner already said in the thread ("the `--replace` flag is also required to trigger it"). My check doesn't separate the main outcome from a side note, so this package sits on the edge, which is why it passed in one run and failed in the other.

**Check rationale**

I picked conventions-followed. Here it is exactly as it reads in my uploaded rubric.md:

| conventions-followed | The contribution policy and comment templates in the Repo facts section, read against the claim comment and repro comment | Passes if every requirement the stated policy places on comments is met, including an AI-assistance disclosure when the policy requires one, or if the repo states no such requirement (silence passes). Fails if the policy requires a disclosure, template, or field and the comments omit it | required |

The eval set has one disclosure package, and without a check like this my rubric couldn't match that category at all. I pointed it at the Repo facts section because every package has a "contribution policy" line there.

I kept it to rules about comments and didn't make it "follow the repo's templates" in general. The bug-report template (like calib-02's "template asks for the operating system, the Joplin version...") is about what an issue should include, not a comment, so a broader check would have failed good packages. "Silence passes" means a repo with "no stated AI policy" never counts against a comment. It matched the disclosure package in both runs ("disclosure 1/1").

**Trade-offs**

One thing conventions-followed will miss: it only sees the policy as written in the Repo facts section. If a repo keeps its disclosure rule somewhere the package doesn't capture, the check passes on silence, and a comment that should have disclosed gets through. I'm okay with that, since grading against rules the package doesn't show would just be guessing.

Between my two full runs, rubric.md didn't change. I only added one sentence to the Environment section of evidence-guide.md. I don't think that edit caused the two new disagreements, because neither one failed on environment-recorded: "pkg-03  accept  reject   NO     failed: outcome-honest" and "pkg-09  accept  reject   NO     failed: behavior-matches-issue". Both packages passed in Run 1 with the same rubric, so I read these as the grader going different ways on borderline calls. The other categories held in both runs ("disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4").

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
