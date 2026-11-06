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

**Unit 7: Wrote my ship manifest and shipped PR #694 through the ship-gate**

My ship manifest runs the three checks the repo’s CI and pre-commit hook use: format:check, npm test, and test:coverage. I left out npm install because it rewrites package-lock.json. Two existing test suites failed on Node 22, and those failures would also have blocked every commit through the pre-commit hook, so I switched to Node 26 to match CI. On my real branch the ship-gate passed all three checks and my pr-precheck, but my voice guard stopped the PR over a claim that had no printed output behind it. After trimming that line and re-running the gate, I opened PR #694.

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

- Tool: issue-scout. I ran one scan, then graded my two Issue Selection picks before and after this week’s scope patch
- What it produced: An accept for #388, which passed every required check and was rated straightforward, and a reject for #386 on “No live claim.”
- Difficulties: My ranking filters barely narrowed the scan, the response check passed on evidence that was mostly from 2024, and my strict “Bounded scope” check would have rejected most real issues
- What changed: I excluded bot authors in every query and replaced “Bounded scope” with the scope-feasible row plus a difficulty note

---

## Understanding the Issue

**Problem Description**

The Cupcake Ipsum Generator page has no Jest tests. Nothing checks that the page renders, that it generates the right number of paragraphs, or that it copies the text, so a change that broke it would still pass CI.

**Expected Behavior**

The page has a test file covering rendering and the user interactions (the count input, Generate, and Copy). The tests pass locally and in CI.

**Current Behavior**

No test in __tests__/ or src/ references the page. `npm test -- __tests__/customizer/CupcakeIpsumGenerator` finds no tests, and page.jsx has 0% coverage across the whole suite.

**Affected Components**

src/app/customizer/CupcakeIpsumGenerator/page.jsx (the page under test; I won't change it) and a new test file at __tests__/customizer/CupcakeIpsumGenerator/page.test.jsx.

**Toolkit**

- Tool: A CLAUDE.local.md repo memory file, built from one scoped orientation run over the Cupcake Ipsum folder and the existing customizer tests.
- What it produced: A map of the project. All of the page’s logic lives in page.jsx (state, generate(), copy(), theme), it says where the new test file goes, and it points to the Readme generator test as the pattern to copy.
- Difficulties: The first version said tests only live in __tests__/, which was wrong; repro-check caught it. Prettier’s format check also flagged my local files.
- What changed: I corrected the memory file and added rules for restoring package-lock.json and for formatting only my local files

---

## Reproduction Process

**Environment Setup**

Environment: macOS 26.5, Node v22.16.0, npm 10.9.2. WebDevTools main at commit ce28cbee88465844869da4603d69e55063bd22aa (Nov 5, 2026). Setup: gh repo fork Bashamega/WebDevTools --clone, cd WebDevTools, npm install.
Issues I hit: npm install rewrote package-lock.json, so I ran git restore package-lock.json to keep it out of my diff. On Node 22, two existing JSON Generator test suites won’t run because the faker package is an ES module. They fail on unmodified main too and have nothing to do with the Cupcake Ipsum page. I also ran my first checks from the wrong folder, then re-ran them inside the clone.

**Steps to Reproduce**

1. `ls __tests__/customizer/`
2. `grep -rl "CupcakeIpsum" __tests__ src --include="*.test.*" || echo "no matches"` (the repo keeps tests in both __tests__/ and next to the code in src/)
3. `npm test -- __tests__/customizer/CupcakeIpsumGenerator`
4. `npm run test:coverage -- --collectCoverageFrom=src/app/customizer/CupcakeIpsumGenerator/page.jsx` (runs the whole suite)

Result: no test file mentions CupcakeIpsum, Jest finds no tests for the page, and page.jsx is at 0% coverage.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:**
Step 1:

    Readme-generator

Step 2:

    no matches

Step 3:

    No tests found, exiting with code 1
    Pattern: __tests__/customizer/CupcakeIpsumGenerator - 0 matches

Step 4:

    File      | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
    All files |       0 |        0 |       0 |       0 |
     page.jsx |       0 |        0 |       0 |       0 | 3-74
    Tests:       5 passed, 5 total

The 2 failed suites are src/app/customizer/JsonGenerator/tests/JsonGenerator.test.js and CardForm.test.js. Both fail to run on unmodified main with:

    Must use import to load ES Module: /Users/fikerkifle/WebDevTools/node_modules/@faker-js/faker/dist/index.js
    
- **My findings:** the issue holds on today's main. The Cupcake Ipsum page (src/app/customizer/CupcakeIpsumGenerator/page.jsx) has no tests anywhere in the repo. I also found that the repo keeps tests in two places, __tests__/ and colocated in src/, and that two unrelated suites already fail on Node 22.


**Toolkit**

- Tool: repro-check. I graded my claim draft alone, then my claim and repro report together.
- What it produced: accept on the claim; two rejects on the repro report, then accept with all six checks passing.
- Difficulties: the first reject was missing output excerpts (a copy error on my end). The second caught a real overclaim: I said no test references the page, but I had only searched __tests__/, and the repo also keeps tests in src/. Its rubric also says "a date" where it means "a delivery date."
- What changed: I pasted the real output, widened my search to src/, and ran coverage on the whole suite, which surfaced two pre-existing test failures on Node 22 that I now report. I also corrected my CLAUDE.local.md.

---

## Solution Approach

**Analysis**

The repo added Jest tests tool by tool through separate issues, and the Cupcake Ipsum page never got one. All of its logic lives in src/app/customizer/CupcakeIpsumGenerator/page.jsx. The page keeps three pieces of state: the paragraph count (cupcakes, a string that starts at 1), the output (cup), and isDarkMode. The generate() function appends one fixed paragraph per cupcake and sets the output. The copy() function writes the output to navigator.clipboard and replaces it with “Text copied successfully”. The theme is read from and saved to localStorage and passed to NavBar.

**Proposed Solution**


Add one test file, `__tests__/customizer/CupcakeIpsumGenerator/page.test.jsx`, following the pattern in `__tests__/customizer/Readme-generator/page.test.jsx` (React Testing Library, localStorage cleared before each test, describe blocks per area). It covers rendering (the count input defaulting to 1, the Generate and Copy buttons), generating (the default gives one paragraph, a count of 3 gives three), copying (capture the generated text before clicking Copy, then assert navigator.clipboard.writeText received it and the page shows "Text copied successfully"), and the theme toggle (found by its "Toggle dark mode" label) saving to localStorage. 


**Implementation Plan**

1. Create a branch named `feature/cupcake-ipsum-tests`, per contributing.md. 
2. Add `__tests__/customizer/CupcakeIpsumGenerator/page.test.jsx` with describe blocks for rendering, generating, copying, and the theme. 
3. Mock navigator.clipboard.writeText and clear localStorage in beforeEach, the way the Readme test mocks browser APIs. 
4. Run `npm test -- __tests__/customizer/CupcakeIpsumGenerator`, then the manifest checks (`npm run format:check`, `npm test`, `npm run test:coverage`). Confirm page.jsx coverage rises from 0% and that generate(), copy(), and the theme toggle are covered. 
5. Format only the new test file with `npx prettier --write` on that path. 

Resolved: NavBar's theme toggle has `aria-label="Toggle dark mode"` in `src/components/navbar.jsx`, the same name the Readme test uses. - The full `npm test` passes only on Node 24.9+. On Node 22, the JsonGenerator and CardForm suites fail to run (already true on main). 
I used Node 26.13.0, matching CI's latest Node. 

Deviation (2026-11-05): I added a sixth test, "a saved dark theme is applied on load," inside the planned theme block, because the toggle test alone didn't exercise the code that reads the saved theme.

**Toolkit**

- Tool: plan-check, which grades my plan.md and plan comment together.
- What it produced: An accept verdict, with all 7 required checks passing. It also answered my one open question by finding NavBar’s “Toggle dark mode” label.
- Difficulties: It caught three problems in my files. Prettier had turned every __tests__ path into bold “tests” locally, my coverage target (“above 0%”) proved too little, and my copy test had to capture the text before clicking Copy. It also named gaps in its own procedure, such as having no step for repro evidence that exists only in a draft.
- What changed: I backticked every path, added a Risks section, named generate(), copy(), and the theme toggle as what the tests must cover, and fixed the step order in the copy test.

---

## Testing Strategy

I re-ran my reproduction on main and on my branch, both on Node 26.13.0. On main (ce28cbe), no test file referenced CupcakeIpsum, npm test -- __tests__/customizer/CupcakeIpsumGenerator found no tests, and page.jsx had 0% coverage. On my branch (25e9a72), that search finds the new test file and all 6 tests pass. page.jsx coverage is now 96.15% of statements and 100% of branches and functions; the only uncovered line is 18, the catch that logs when a saved theme can’t be read. The repo checks from my manifest also pass on the branch: npm run format:check, npm test (10 suites, 42 tests), and npm run test:coverage. The pre-commit hook ran the format check and the full suite before it let me commit.


**Toolkit**

- Tool: My ship manifest. It lists the three checks from the repo’s CI and pre-commit hook, plus the coverage run from my reproduction.
- What it produced: Before-and-after evidence in test_evidence.md, and passing runs of all three manifest checks on my branch.
- Difficulties: My first format check flagged the evidence file because I was still writing it. Separately, the full test suite only passes on Node 24.9 or later.
- What changed: I formatted the evidence file, re-ran the format check, and recorded both runs. I also switched to Node 26 to match CI.

---

## Implementation Notes

2026-11-05: Switched from Node 22 to Node 26.13.0. The repo’s pre-commit hook runs the full test suite, and on Node 22 two existing JSON Generator suites fail to load the faker package, which would have blocked every commit. CI uses the latest Node, so this also matches CI.

2026-11-05: Created the branch feature/cupcake-ipsum-tests and added __tests__/customizer/CupcakeIpsumGenerator/page.test.jsx, with 6 tests in 4 blocks (rendering, generating, copying, theme). An AI assistant drafted the file from page.jsx and the Readme generator test; I ran it and checked each test against the page’s behavior. The copy test captures the generated text before clicking Copy, because Copy replaces it with a confirmation.

2026-11-05: One of the six, “a saved dark theme is applied on load,” wasn’t in my plan, so I recorded it as a deviation. I noticed the page’s class string is missing a space (“text-gray-400min-w-80”) and left it alone as out of scope. The pre-commit hook passed (10 suites, 42 tests), and I committed as 25e9a72.


**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool: My CLAUDE.local.md memory file, and Claude, which drafted the test file. I ran the tests and verified them myself.
- What it produced: A 115-line test file with 6 passing tests, committed as 25e9a72.
- Difficulties: The repo’s pre-commit hook was blocked on Node 22. Before that, Prettier had mangled the __tests__ paths in my local notes.
- What changed: I upgraded Node and now keep paths in backticks. I didn’t fix the page’s class-string bug because it was out of scope.

---

## Pull Request

**PR Link:** https://github.com/Bashamega/WebDevTools/pull/694

**PR Description:** Adds tests/customizer/CupcakeIpsumGenerator/page.test.jsx, with 6 tests covering rendering, generating, copying, and the theme, following the pattern of the Readme generator’s test. page.jsx is unchanged. There’s no docs change because contributing.md already documents running the tests (#692).
The description shows before-and-after output (no tests and 0% coverage before, 6 passing tests and 96.15% coverage after) and the repo’s checks passing: format:check, npm test with 10 suites and 42 tests, and test:coverage. It says “Fixes #388”. In Notes for Reviewers, I disclose my AI use and flag a class-string bug in the page that’s out of scope here.

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** Awaiting review

**Toolkit**

- Tool: The ship-gate. It runs the three repo checks in my manifest, then my pr-precheck, and only then lets gh pr create run. My voice guard checks the PR description.
- What it produced: A PASS on my branch. The format check, tests, and coverage all passed, and pr-precheck passed every check.
- Difficulties: My voice guard blocked my first PR attempt. One line in Notes for Reviewers claimed Node 22 test failures with no printed output behind it, which breaks a rule I set myself. pr-precheck had already flagged that line, but only as a non-blocking note. Opening the PR on the original repo from my fork also meant passing --repo, --base, and --head to gh.
- What changed: I cut the line down to what my output shows, re-ran the ship-gate, got a second PASS, and opened PR #694.

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
