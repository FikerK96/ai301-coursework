# Plan: Add snapshot tests for prompt templates (#12)

## Diagnosis

The suite cannot catch a template content change, because the one test meant to do it never compares the hash to anything. From my repro on commit `2f4e82f`, I changed `4. Framework and tool mastery` to `4. Framework and tool mastery (content changed, version still v1)` in `skills_feedback` `"v1"` (`rag/generator/prompt_templates.py`, line 21), and the same test file still passed:

```
37 passed in 0.09s
```

`test_template_snapshot_content_hash` computes a hash of the templates but only asserts its shape:

```
assert isinstance(content_hash, str)
assert len(content_hash) == 32  # MD5 hash length
```

Both are true for any MD5 hash of any input, so the test passes whatever the templates contain. The cause is the missing comparison against a stored expected value, not the templates themselves.

## Scope

In: replace the shape-only assertions in `test_template_snapshot_content_hash` with a comparison of each template's content hash against a stored expected hash, keyed by template name and version. A template whose content changes under an existing version key fails. A new version key with no recorded hash also fails, so adding a version is a conscious step.

Out: any edit to the templates or to `rag/generator/prompt_templates.py`, any new test dependency (no snapshot library; standard library `hashlib` only), CI configuration, and the other tests in the file.

## Files to touch

- `tests/unit/test_prompt_templates.py`: rewrite `test_template_snapshot_content_hash` and add a module-level dict of expected hashes, `{(template_name, version): md5_hex}`, next to it.

No other files.

## Approach

1. Read `rag/generator/prompt_templates.py` to pin the name of the templates dict and confirm its shape (`{name: {version: content}}`, as line 21's `"skills_feedback": {"v1": ...` suggests), and read how the existing test builds its hash.
2. Compute the MD5 of each template's content with the current, unmodified templates on `main`, and record each one in the expected-hashes dict.
3. Rewrite the test to loop over every (name, version) pair. It fails when the pair has no recorded hash, or when its hash differs from the recorded one. The failure message names the template and version and says to add a new version key and record its hash, rather than editing the content in place.
4. Run the test file and the full unit suite (`make test-unit`) to confirm everything passes on unmodified templates.
5. Follow docs/CONTRIBUTING.md: work on branch `test/12-prompt-template-snapshots`, write Conventional Commits (`test(rag): ...`), give the rewritten test a Google-style docstring, and run `make check && make test-unit` before pushing.

## Test plan

Re-run my unit 2 repro steps against the change:

1. `.venv/bin/pytest tests/unit/test_prompt_templates.py -q`. Expect all tests pass.
2. Make the same edit on line 21 (`4. Framework and tool mastery` → `4. Framework and tool mastery (content changed, version still v1)`), leaving `"v1"` alone.
3. Re-run the same command. Expect `test_template_snapshot_content_hash` to fail, naming `skills_feedback` `v1`. Before the fix, this step showed `37 passed`.
4. Revert the edit and re-run. Expect all tests pass.
5. Add the edited content as a new `"v2"` key for `skills_feedback`, without recording its hash. Expect a failure naming `skills_feedback` `v2` as unrecorded. Record its hash, re-run, and expect a pass. Then remove the `"v2"` key and its hash.
6. Run `make check && make test-unit` on unmodified templates. Expect lint, format, typecheck, and the unit suite all to pass, matching the CI jobs CONTRIBUTING.md requires.

## Risks and unknowns

- Unknown until step 1 of the approach: whether every template is a plain string, or whether some are built or formatted at import time. If any are, the hash must be computed on the stored template, not a rendered prompt, or the test will be flaky.
- Unknown: whether maintainers prefer hashes stored in the test file or in a separate snapshot file. I'm keeping them in the test file, the only file the issue lists, and will say so in the PR.
- Risk: future template edits now require updating a hash. That is the issue's intent, and the failure message says exactly what to do.

## Deviations

- Resolved unknown: `PROMPT_TEMPLATES` in `rag/generator/prompt_templates.py` holds 5 plain string literals (`first_impression`, `gaps_feedback`, `presentation_feedback`, `projects_feedback`, `skills_feedback`), each with only a `v1` key. Nothing is built at import time, so hashing the stored strings is safe, and the first risk under Risks and unknowns did not apply.
- Test plan step 6 did not fully hold locally. Ruff and black pass, `tests/unit/test_prompt_templates.py` gives 37 passed, and `make test-unit` gives 375 passed and 53 xfailed. `make typecheck` in my local `.venv` fails inside numpy's type stubs (`numpy/__init__.pyi:737: Type statement is only supported in Python 3.12 and greater`), and it fails the same way with my change set aside, so it comes from my local environment, not this change. The repo's pre-commit mypy hook, which runs in its own environment, passed on my commit (`ee635b7`). Fixing the local mypy setup is outside this plan's scope; I will note it in the PR, as docs/CONTRIBUTING.md asks for failures I can't connect to my diff.
- Added beyond the plan: the rewritten test collects every failing (name, version) pair before asserting, so one run reports all changed or unrecorded templates instead of stopping at the first. This does not change what the test catches.
- Otherwise built as planned: one file changed (`tests/unit/test_prompt_templates.py`), the same approach, and the same test plan. My posted plan comment on #12 is still accurate, so no follow-up comment is needed.
