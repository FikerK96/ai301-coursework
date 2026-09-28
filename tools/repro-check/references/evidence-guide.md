# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the Issue section, the Repo facts section, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

- Where it lives: In an eval bundle, the repro report's environment record, compared against the Issue section (the version, OS, runtime, or commit the issue names) and the Repo facts section (supported versions). In live mode, the draft report's environment section, compared against the issue thread and the repo's setup docs.
- What good looks like: Every component the issue's behavior depends on (OS, language runtime, package or app version, commit or branch) is named with a specific value, and each one matches what the issue targets or the difference is called out. The fields listed in the Repo facts section's bug-report template (for example, OS and app version) count as components the behavior depends on. "Latest" or "my machine" is not a value.

## Steps

- Where it lives: In an eval bundle, the repro report's steps, from the stated starting state to the trigger. In live mode, the draft report's steps, checked against the repo's own setup docs.
- What good looks like: Someone who has never seen the repo could start from the stated starting state (for example, a fresh clone at a named commit) and reach the trigger without guessing. Every command, input, and setting that the result depends on is written out. Setup the repo's docs already cover may be cited by link rather than repeated.

## Behavior shown

- Where it lives: In an eval bundle, the artifacts in the repro report (output excerpts, logs, screenshots, observed-behavior text), read against the issue's description of the bug. In live mode, the same artifacts in the draft, read against the issue thread's description.
- What good looks like: The artifact shows the same symptom the issue describes: the same error message, the same wrong value, or the same failing path. An error from a different component, a different message, or a setup failure before the trigger is an adjacent behavior and does not count. For a cannot-reproduce, the artifact shows what actually happened at the step where the issue says it breaks.

## Honesty

- Where it lives: In an eval bundle, the report's outcome statement and any stated cause, set against its own artifacts. In live mode, the same in the draft report and repro comment.
- What good looks like: Every outcome claim points to an artifact in the package that shows it. "Reproduced" needs an artifact showing the issue's behavior. "Could not reproduce" needs the environment and an artifact showing what happened instead, and passes when it has them. A root cause is only stated as fact if something in the package demonstrates it; otherwise it is labeled a guess or left out.

## Comms

- Where it lives: In an eval bundle, the claim comment read against the issue, and both comments read against the contribution policy and templates in the Repo facts section. In live mode, the draft comments read against the issue thread, the repo's CONTRIBUTING file and issue templates, and scope.md's house rules.
- What good looks like: The claim names this issue's specifics and promises only investigation and a report, never a fix or a date. Each comment stands on its own words rather than pointing at someone else's repro. Every requirement the repo's policy places on comments is met; in particular, if the policy requires disclosing AI assistance, the comment discloses it. A repo with no stated requirement imposes none.