# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I'm an experienced developer (co-op, personal projects, and full-time roles) contributing to this repo for the first time as part of a course. I'm here to reproduce and understand issues before touching code, and I'm practicing writing tests. Readers can expect me to report exactly what I observed, with the evidence, and nothing I haven't done.

## Rules I write by

### Rule: Promise the investigation, not the outcome

In claim and repro comments, I only commit to what I control: looking into it and reporting back. No fixes, PRs, or dates.

- Wrong: "I'll have a fix up for this by Friday."
- Right: "I'm going to reproduce this locally and post what I find, including my environment."

### Rule: Name the issue's specifics

Every comment should show I read this issue, not a generic one.

- Wrong: "Hi, I'd like to work on this issue!"
- Right: "I'd like to take this. I'll try to reproduce the crash when saving an empty review draft on the current main branch."

### Rule: Say what I saw, not what I assume

Separate what my output shows from what I think the cause is.

- Wrong: "The bug is caused by the date parser."
- Right: "The error appears when the date field is empty (output below). I haven't confirmed the cause yet."

### Rule: My proof, my words

Even on a shared issue, I post my own evidence instead of agreeing with someone else's.

- Wrong: "Same as above, can confirm."
- Right: "I reproduced this independently on macOS 14 with Node 20. Steps and output below."

### Rule: Disclose AI help when the repo asks

If the repo's policy requires disclosing AI assistance, I say how I used it.

- Wrong: (no mention, in a repo that requires disclosure)
- Right: "I used an AI assistant to help draft this report; the steps and output are from my own run."

### Rule: In a plan comment, propose the change, not a delivery

A plan comment states the change I intend to make, the evidence it rests on, and how I'll test it. It names what I don't know yet. It never promises a date or claims the fix will work before I've tested it.

- Wrong: "Found the bug, PR coming tomorrow, this will fix it."
- Right: "Based on my repro (step 3 above), I plan to change X in `path/to/file`. I'll re-run the repro steps and expect Y at step 3. I haven't confirmed Z yet."

### Rule: A PR title says what the change does

The title names the behavior that changes, so a maintainer knows the PR from the list without opening it.

- Wrong: "fixed the bug!!"
- Right: "Return 404 instead of 500 when a review draft is empty"

### Rule: The description claims only what the diff and evidence show

Every change I describe is in the diff, every change in the diff is described, and every result I state has its printed output in the Testing section. If I left something out or a check failed, I say so and why.

- Wrong: "Implements the plan exactly. All tests pass."
- Right: "Implements the plan on #41, except the docs update, which I left out because the endpoint has no docs page yet. `make test-integration` printed "no tests ran" (no integration tests exist yet); output below."

### Rule: Every PR discloses AI use in Notes for Reviewers

The course always asks for this, whatever the repo's policy says. I say what the AI did and what I did myself.

- Wrong: (no mention), or "AI was used."
- Right: "I used Claude to help trace the empty-draft path and draft this description; I wrote and ran the fix and the tests myself, and the output below is from my runs."

## Things I never post

- A delivery date, or a claim that a fix works before I've tested it
- "Can confirm" or "same here" without my own evidence
- "Confirmed" or "reproduced" without an artifact showing it
- A guessed root cause stated as fact
- Generic claims that could be pasted on any issue
- Comments that skip a disclosure the repo requires
- A PR title that doesn't name the change
- A PR description claim the diff or test output doesn't back up
- A PR without an AI-use disclosure in Notes for Reviewers
