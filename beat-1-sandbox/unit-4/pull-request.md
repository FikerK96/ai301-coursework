# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/154

**Branch**

test/12-prompt-template-snapshots

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

RUN 1 (full run): 13/20
clear-accept 0/7
not-tested 4/4
silent-drift 4/4
standards-wall 2/2
unreviewable 3/3

RUN 2 (pkg04,pkg07,pkg03,calib02,calib04 + 7 NO ROWS): 9/10
pkg05 still reject on evidence_observable

RUN 3 (full run): 19/20
clear-accept 6/7
not-tested 4/4
silent-drift 4/4
standards-wall 2/2
unreviewable 3/3

**Package analysis**

pkg-05 (nushell/nushell#18848, clear-accept). My rubric decided reject; the gold label is accept. It failed only `evidence_observable`.

The plan's test plan names two proof items: "re-run the issue's script, expect both `atuin` rows; re-run with two same-name same-key bindings, expect one row plus a warning". The first has printed before/after tables. The second appears only as one sentence: "Same-key redefine prints the one-time warning." There is no command and no output for it.

My check requires that "every other repro or failure mode the test plan names as proof is reported with its observed result", and it fails "when the after is only a verdict with no observation". The grader read "prints the one-time warning" as a verdict on a named proof item rather than an observation, so it failed the check. The gold label treats the sentence as a sufficient report on a secondary item, since the main repro is fully proven with printed output. The same clause is what correctly rejects calib-04, which never reports its second failure mode (`-j 200000 -x echo .`), so I kept it.

**Check rationale**

| evidence_observable | The Test evidence, read against every repro or failure mode the Test plan in Plan context names as proof of the fix, with Plan context's repro evidence as the before | The issue's own repro is reported as re-run on the change, with its command or steps and a concrete observed after result (printed output, or a specific observation such as "no error, searches normally" or "browser shows the full URL") that differs from the before the way the test plan predicts; every other repro or failure mode the test plan names as proof is reported with its observed result, or its omission is stated with a reason in the Description; fails when evidence is absent, when the after is only a verdict with no observation ("works", "fixed", "should be fine", "looks right"), when the issue's repro was not re-run, or when a named failure mode is silently left out; controls and smoke checks may be stated briefly | required |

My first version, built from the class worksheet's rule ("A note after # saying what it printed doesn't count"), required that the after appear "as a command with its actual printed after output" and said "an after given only as a sentence or a # note is not proof". Run 1 showed that was too strict: gold-accept packages report the after as a specific observation in a note, such as pkg-11's "# after: searches normally, no error" and pkg-13's "browser shows https://duckduckgo.com/?q=hello&t=brave", and my rubric rejected them. So I moved the line from printed vs. unprinted to concrete observation vs. bare verdict. I kept "silently left out" because calib-04 shows repro 1 but never repro 2, and kept the "only a verdict" clause because calib-03's "# after: matches the issue's expected output byte for byte" and calib-02's "did not get a chance to test" must still fail.


**Trade-offs**

Loosening `evidence_observable` and `repo_checks_run` traded verifiability for agreement: a stated observation can't be checked against real output, so a confidently worded false claim can now pass. To make sure the loosening didn't let real not-tested or drifting PRs through, I re-ran canaries with `--only`: pkg-04 and pkg-07 (not-tested), pkg-03 (silent-drift), and calib-02 and calib-04 (calibration traps). All five stayed reject, and the confirming full run kept not-tested at 4/4 and silent-drift at 4/4. The case I accept missing is pkg-05: loosening further to pass its one-sentence warning claim would also pass not-tested packages whose whole problem is outcomes stated without proof, so I left it as the one disagreement.


---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
