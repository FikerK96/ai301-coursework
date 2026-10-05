# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

FikerK96

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5987094952

Plan for #12, built on [my reproduction](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5863802231) (commit `2f4e82f`): editing `skills_feedback` `"v1"` content on line 21 of `rag/generator/prompt_templates.py` without a version bump left `tests/unit/test_prompt_templates.py` at `37 passed`.

**Cause:** `test_template_snapshot_content_hash` computes an MD5 of the templates but only asserts `isinstance(content_hash, str)` and `len(content_hash) == 32`, so it can never fail.

**Change:** in `tests/unit/test_prompt_templates.py` only, replace those assertions with a comparison of each template's hash against a stored expected hash keyed by template name and version. Changed content under an existing version fails, and a new version with no recorded hash fails, so versioning becomes a conscious step. No changes to the templates themselves, no new dependencies, no CI changes.

**Test:** re-run my repro. After the fix, the same line 21 edit should fail the test, naming `skills_feedback` `v1`, where it passed before. I'll also check that a new `v2` key fails until its hash is recorded, and run `make check && make test-unit` per CONTRIBUTING.md. Branch: `test/12-prompt-template-snapshots`.

**Open questions:** I still need to confirm every template is a plain string rather than built at import time. I'm keeping the expected hashes in the test file, since it's the only file the issue lists; happy to move them to a snapshot file if maintainers prefer.


---

## Your branch

**Branch**

test/12-prompt-template-snapshots

**Evidence**

**Before the fix** (from my unit 2 repro comment, commit `2f4e82f` on `main`):

```
$ .venv/bin/pytest tests/unit/test_prompt_templates.py -q
37 passed
```

Edited `rag/generator/prompt_templates.py` line 21: `4. Framework and tool mastery` → `4. Framework and tool mastery (content changed, version still v1)`, leaving the `"v1"` key alone, then re-ran the same command:

```
$ .venv/bin/pytest tests/unit/test_prompt_templates.py -q
.....................................                                    [100%]
37 passed in 0.09s
```

**After the fix** (branch `test/12-prompt-template-snapshots`, commit `ee635b7`):

```
$ .venv/bin/pytest tests/unit/test_prompt_templates.py -q
.....................................                                    [100%]
37 passed in 0.13s

$ git diff rag/generator/prompt_templates.py
diff --git a/rag/generator/prompt_templates.py b/rag/generator/prompt_templates.py
index d3cdde8..47bfff2 100644
--- a/rag/generator/prompt_templates.py
+++ b/rag/generator/prompt_templates.py
@@ -18,7 +18,7 @@ Based on the portfolio evidence above, provide structured feedback on:
 1. Demonstrated technical skills (with specific examples from projects)
 2. Depth of expertise in key areas
 3. Programming language proficiency
-4. Framework and tool mastery
+4. Framework and tool mastery (content changed, version still v1)
 
 Format your response as JSON with these fields:
 - key_skills: list of demonstrated skills with evidence

$ .venv/bin/pytest tests/unit/test_prompt_templates.py -q
.........................F...........                                    [100%]
=================================== FAILURES ===================================
___________ TestPromptTemplates.test_template_snapshot_content_hash ____________

self = <tests.unit.test_prompt_templates.TestPromptTemplates object at 0x109f205f0>

    def test_template_snapshot_content_hash(self):
        """Snapshot test: each template's content matches its recorded hash.
    
        Compares the MD5 of every (template_name, version) pair in
        PROMPT_TEMPLATES against EXPECTED_TEMPLATE_HASHES. Fails when a
        template's content changed under an existing version, or when a
        version has no recorded hash.
    
        Raises:
            AssertionError: If any template is unrecorded or its hash differs.
        """
        failures = []
        for name in sorted(PROMPT_TEMPLATES.keys()):
            for version in sorted(PROMPT_TEMPLATES[name].keys()):
                content_hash = hashlib.md5(PROMPT_TEMPLATES[name][version].encode()).hexdigest()
                expected_hash = EXPECTED_TEMPLATE_HASHES.get((name, version))
    
                if expected_hash is None:
                    failures.append(
                        f"{name} {version} has no recorded hash. If this is a "
                        f"new version, add ({name!r}, {version!r}): "
                        f"{content_hash!r} to EXPECTED_TEMPLATE_HASHES."
                    )
                elif content_hash != expected_hash:
                    failures.append(
                        f"{name} {version} content changed (expected hash "
                        f"{expected_hash}, got {content_hash}). Don't edit an "
                        f"existing version in place: add a new version key and "
                        f"record its hash in EXPECTED_TEMPLATE_HASHES."
                    )
    
>       assert not failures, "\n".join(failures)
E       AssertionError: skills_feedback v1 content changed (expected hash f93103d823482a2e65decc6653e4ee5c, got 1854374938042fc9e189237b53598128). Don't edit an existing version in place: add a new version key and record its hash in EXPECTED_TEMPLATE_HASHES.
E       assert not ["skills_feedback v1 content changed (expected hash f93103d823482a2e65decc6653e4ee5c, got 1854374938042fc9e189237b53598128). Don't edit an existing version in place: add a new version key and record its hash in EXPECTED_TEMPLATE_HASHES."]

tests/unit/test_prompt_templates.py:233: AssertionError
=========================== short test summary info ============================
FAILED tests/unit/test_prompt_templates.py::TestPromptTemplates::test_template_snapshot_content_hash
1 failed, 36 passed in 0.13s

$ git checkout -- rag/generator/prompt_templates.py
$ .venv/bin/pytest tests/unit/test_prompt_templates.py -q
.....................................                                    [100%]
37 passed in 0.11s
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1: 17/20
clear-accept 4/7
scope-creep 4/4
thread-convention 2/2
unbuildable 3/3
wrong-cause 4/4

Run 2 (pkg-03,13,14,10,01): 5/5
Changes: stranger_can_start, unknowns_stated

Run 3: 20/20


**Package analysis**

pkg-14. In Run 1 my rubric rejected it (`failed: stranger_can_start, unknowns_stated`), but the gold label is accept. In Run 2 my rubric accepted it, matching gold.

Why Run 1 rejected it: the plan names the area and the approach, but leaves the exact edit site open: "exact functions to be pinned in the PR after tracing the query issuance with debug logs, which I have working (the leak's origin is visible in `zellij --debug` output)." My `stranger_can_start` check then required that "A stranger could make the first edit without asking a question, and the files named exist in the repo," read against the repo-facts block. The plan doesn't name the exact function for the first edit, and the repo-facts block lists no file paths, so the grader could not pass it. `unknowns_stated` then required that "Anything the evidence does not establish is stated as an unknown, not asserted as fact," most likely because the plan's mechanism ("the responses arrive as ordinary input and are echoed into the active pane") is an inference from the repro, not something the repro shows directly.

Why gold accepts it: a stranger can still start, because the plan gives the concrete step that pins the open detail (trace with `zellij --debug`). And it is honest about what it doesn't know: it defers the Windows variant ("I cannot test Windows; the fix site may be shared") and names its risk ("draining input at attach risks eating one legitimate keystroke"). After I revised both checks, my rubric reads it the same way.

**Check rationale**

| stranger_can_start | The plan's change: the files, function or area, and approach it names | A stranger could begin the work without asking the author a question: the plan says where the change goes and what the change is, or names the concrete step that will pin down any detail still open | required |

It reads this way after two revisions. The first version was: "A stranger could make the first edit without asking a question, and the files named exist in the repo," with evidence "read against the repo-facts block." In Run 1 it rejected three gold-accept plans (pkg-03, pkg-13, pkg-14). The cause was the file-existence clause: the repo-facts block in the packages (e.g. calib-01) lists stars, release, templates, and contribution policy, but no file paths, so the grader had nothing to confirm a path against. I dropped that clause and pointed the evidence at the plan's change itself.

I rejected an intermediate version ("the plan says where the change goes and what the change is") because pkg-14 would still fail it: pkg-14 leaves exact functions "to be pinned in the PR after tracing," and gold accepts it. So I added "or names the concrete step that will pin down any detail still open." That keeps the failure family it targets (a plan a stranger could not start executing) without holding plans that are honest about one open detail and say how they'll close it.

**Trade-offs**

Loosening `stranger_can_start` risked letting unbuildable plans through, so I re-ran pkg-10 (unbuildable, already agreeing) as a canary with `--only` alongside the three misses. It still rejected, and Run 3 kept unbuildable at 3/3, so the change didn't flip any package that agreed before.

What it gives up: the check can no longer catch a plan that names a file that doesn't exist, because the eval packages give the grader no file tree to check against. And a plan could name a vague "step" (e.g. "investigate further") and the grader might count it as concrete. I accept those misses because the alternative, the original check, held honest gold-accept plans (3 of 7 clear-accept in Run 1).

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
