# Contribution: Implement Jest Tests for Cupcake Ipsum Generator

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Fiker Kifle
**GitHub Username:** FikerK96
**Issue:** https://github.com/Bashamega/WebDevTools/issues/388
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout and tested it on a real scan**

I built issue-scout: a fit profile, seven gh search issues queries, and ranking filters that pass the top 5 results to my rubric for grading. In the first scan, the ranking filters barely narrowed anything, so a bot-filed issue got through. The rubric also passed an issue with an open decision in its body, and it passed repos that had no maintainer response to judge. Now every query excludes bot authors, the scope check fails any issue with an unanswered open decision, and “nothing to judge” counts as a fail.

**Unit 6: Added the voice guard and a repo memory file for WebDevTools

I installed the voice guard, which checks every comment I post through Claude Code against my voice guide, and added upstream rules for claims, questions, and pings. Setup showed my guide had drifted into three copies, so I folded the newest one back into a single file. The guard stopped the wiring test as expected and passed my real claim on #388, which its log confirms.

I also wrote a CLAUDE.local.md for WebDevTools from one scoped orientation run. That run found all of the Cupcake Ipsum logic lives in a single page.jsx, so my test plan targets one file.

My claim also passed repro-check, though its rubric says “a date” where it means “a delivery date,” and I’d reword that.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I ran my issue-scout with seven gh search issues queries built from my fit profile: Python, Java, TypeScript, and SQL, and worked on tests, docs, and small fixes. It graded 5 of the 582 results and accepted 4. My actual issue had to come from the AI301 Issue Selection site, though, so I filtered that list by my languages and the documentation, tests, and bug tags. I dropped my first pick, proCAT#857, after its maintainer asked outside contributors not to take those issues. Then I graded two Jest-test issues in Bashamega/WebDevTools. The scout accepted #388 (Cupcake Ipsum Generator tests) with the difficulty note “straightforward,” and rejected #386 because someone had claimed it earlier that day.
#388 fits my profile. I want practice writing tests, the repo’s JavaScript/React stack is close to my TypeScript work, and a recently merged PR (#692) shows the test pattern to follow. I’m hoping to get comfortable with React Testing Library and with covering a component’s rendering and interactions.
On claims, the scout did well: it caught the fresh claim on #386, which the site’s list didn’t show. Its ranking filters barely narrowed the first scan, though. The maintainer-response check also passed WebDevTools mostly on 2024 evidence, while recent outside PRs (#626 to #628) are still unreviewed, so I can’t count on a quick review. I’ve excluded bot authors from my queries and replaced the strict scope check with the scope-feasible row. Next I’d weight the response check toward recent activity.
Claim comment: https://github.com/Bashamega/WebDevTools/issues/388#issuecomment-6667161459

**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: [the scan and its verdict on this issue, described]
- Difficulties: [where it fell short, or "none met" if none did]
- What changed: [what you patched or would update, or "nothing"]

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool: issue-scout. I ran one scan, then graded my two Issue Selection picks before and after this week’s scope patch
- What it produced: An accept for #388, which passed every required check and was rated straightforward, and a reject for #386 on “No live claim.”
- Difficulties: My ranking filters barely narrowed the scan, the response check passed on evidence that was mostly from 2024, and my strict “Bounded scope” check would have rejected most real issues
- What changed: I excluded bot authors in every query and replaced “Bounded scope” with the scope-feasible row plus a difficulty note

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
