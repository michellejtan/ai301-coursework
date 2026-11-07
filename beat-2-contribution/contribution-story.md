# Contribution: Add a constants file for python modules

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Michelle Tan
**GitHub Username:** michellejtan
**Issue:** https://github.com/ESCOMP/CTSM/issues/1621
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

**Unit 5: Built issue-scout with my own queries and filters, then fixed it when it favored day-old issues**

I wrote a search strategy with JavaScript and Python queries traced to my fit profile and filters that drop assigned and stale issues, keep one issue per repo and sort by fewest comments, then ran the scout. The first scan accepted all five issues, but every one was under two days old in a repo with 0 to 12 stars, because "fewest comments first" rewards brand-new issues, so I added `--created "<2026-10-17"` to both queries and removed a Go/Rust/Java drop rule that can't be checked from search results. My first rescan returned the identical top five because the scout reused cached evidence; I caught it by running the new query myself, saw none of those issues came back, and re-ran with an instruction to search fresh. The fresh scan surfaced older issues and the rubric rejected the bad ones (a repo dead since 2018, an issue with an open PR, one with four unrelated asks), so I left the rubric alone.

**Unit 6: Installed a voice guard with an Upstream section and wrote a CTSM memory file that records the maintainer's AI rule**

I added an Upstream section to my voice guide and installed the hook; its log shows it stopping `gh issue comment --help` in my wiring test (that is the intended result: there is no comment text to check, so the guard blocks on purpose instead of letting an unreadable command through) and, on 2026-11-03, stopping a claim draft for "a promised delivery date for a fix I haven't started" until I fixed it. It fell short because it can't see my browser, so a comment I post in the browser only gets checked if I run `check_voice.py --draft` myself; I posted my question on #1621 first and ran the check afterward, and it passed. While writing the memory file (`CLAUDE.local.md`, 26 lines, kept out of my PR with `.git/info/exclude`), my orientation showed that most of #1621 was already done in `pft_utils.py`, so I asked the maintainer about scope instead of building what my claim described. ekluzek also pointed me to PR #4286, which says LLMs must not post to issues or PRs, so I wrote this rule to my memory file: Claude can write drafts, but I must review, edit, and post everything myself.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I found this issue by scanning all of GitHub with my own scout: `gh search issues` queries for open "good first issue" Python and JavaScript issues, then grading the top results against my rubric. The first scan was mostly day-old issues in tiny repos, so I added a creation-date cutoff and re-ran it fresh. When I graded my real picks, the scout rejected MaterialX#2813 (an open draft PR already said it fixes the issue, and a stranger had claimed it) and MFC#2086, and accepted CTSM#1621. I graded CTSM#1621 and devtrack#162 again after patching my rubric this week. The scout accepted CTSM#1621 with the difficulty note "moderate": the issue doesn't say where the new file goes, several Python modules are involved, and ekluzek asked for the branch and PR to be based on `b4b-dev`. I chose it because it's a small, well-defined Python task (a shared constants module for NATPFT, MXPFT and MONTHS_PER_YEAR), and Python is the language I'd like to build on. It's also in a large scientific codebase, which is new to me. I hope to learn how a large project structures shared code, how a bit-for-bit (b4b) branch workflow works, and how to propose a file location and naming to a maintainer before I write code. I claimed the issue on 2026-11-01 and ekluzek, a CTSM contributor, replied within about two hours: https://github.com/ESCOMP/CTSM/issues/1621#issuecomment-6550957028

I also graded devtrack#162, and the scout rejected it only because the repo auto-assigned the issue to me after I claimed it. The rubric's `unassigned` check can't tell my own assignment from a stranger's, and I didn't change the rubric for that, so my pick was not made against the scout's verdict. On a real wild search, the scout held up on the rejections I could check by reading the threads. It fell short in places: it often left maintainer-response "unclear" because it never pulled the reply-time sample, it flagged my own claim as a failed no-recent-claim check, and once it reused cached evidence until I told it to search fresh. The scope check I replaced, bounded-change, might have rejected this issue, because it has an open design edge (the file location and the best way to define the constants aren't decided).

**Toolkit**

- Tool: issue-scout (my search strategy and my rubric), run as a scan, then as `issue-scout: grade <issue URLs>` on my picks.
- What it produced: a scan of older Python and JavaScript good-first-issue candidates, then graded read-outs for my picks. For CTSM#1621 it gave accept with difficulty "moderate", and it rejected devtrack#162 because I was auto-assigned to it.
- Difficulties: it treats my own claim and assignment like a stranger's, maintainer-response was often "unclear" because the reply sample wasn't pulled, and it once reused cached evidence until told to run fresh. It also reported a commit date one day in the future.
- What changed: I replaced the bounded-change check with scope-feasible plus a difficulty note, and logged the rest in scan-notes.md. I would exempt my own account from `unassigned` and `no-recent-claim`.

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

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

Ubuntu on WSL2 (Linux 6.18), Python 3.12.3, zsh. I forked ESCOMP/CTSM (leaving "copy the master branch only" unchecked so the fork has `b4b-dev`), cloned my fork, added the upstream remote, and made a branch from `upstream/b4b-dev` at commit 23baa191e (2026-11-03). This issue is about where constants are defined, so I only searched the source and git history; I did not build the model, use the conda environment, or run the CTSM tests. The issue states no target version, so there is no version gap. One challenge: my first grep failed in zsh because the unquoted `--include=*.py` was expanded as a file glob, so I quoted the pattern.

**Steps to Reproduce**

1. `git clone https://github.com/michellejtan/CTSM.git && cd CTSM`
2. `git remote add upstream https://github.com/ESCOMP/CTSM.git && git fetch upstream`
3. `git checkout -b constants-module upstream/b4b-dev`
4. `grep -rn "MONTHS_PER_YEAR" --include="*.py" . ; echo "exit=$?"`
5. `grep -rn "range(1, 13)" --include="*.py" python/ctsm | grep -v /test/`
6. `sed -n 1,12p python/ctsm/pft_utils.py`
7. `grep -rn "pft_utils" --include="*.py" python/ctsm | grep -v /test/`
8. `git log --format="%h %ad %an %s" --date=short -3 -- python/ctsm/pft_utils.py`

Observed result: step 4 finds no `MONTHS_PER_YEAR` (`exit=1`); step 5 finds the month range hard-coded three times in one module; steps 6-8 show the PFT constants already live in a shared `pft_utils.py`, imported by four modules.

**Reproduction Evidence**

- **Commit showing reproduction:** none (this was a text search, so I made no commit).
- **Screenshots/logs:**
  ```
  $ grep -rn "MONTHS_PER_YEAR" --include="*.py" . ; echo "exit=$?"
  exit=1

  $ grep -rn "range(1, 13)" --include="*.py" python/ctsm | grep -v /test/
  python/ctsm/cplhist/cplhist_monthly_clim.py:130:    return [(year, month) for year in range(begyr, endyr + 1) for month in range(1, 13)]
  python/ctsm/cplhist/cplhist_monthly_clim.py:751:            for month in range(1, 13)
  python/ctsm/cplhist/cplhist_monthly_clim.py:833:        clim_files = [clim_file(self.mondir, month) for month in range(1, 13)]

  $ sed -n 1,12p python/ctsm/pft_utils.py
  MIN_PFT = 0  # bare ground
  MIN_NAT_PFT = 1  # minimum natural pft (not including bare ground)
  MAX_NAT_PFT = 14  # maximum natural pft
  MAX_PFT_GENERICCROPS = 16  # for runs with generic crops
  MAX_PFT_MANAGEDCROPS = 78  # for runs with explicit crops

  $ grep -rn "pft_utils" --include="*.py" python/ctsm | grep -v /test/
  python/ctsm/subset_data.py:73:from ctsm.pft_utils import MAX_PFT_GENERICCROPS, MAX_PFT_MANAGEDCROPS
  python/ctsm/toolchain/gen_mksurfdata_namelist.py:18:from ctsm.pft_utils import MAX_PFT_GENERICCROPS, MAX_PFT_MANAGEDCROPS
  python/ctsm/site_and_regional/single_point_case.py:19:from ctsm.pft_utils import MAX_NAT_PFT, MAX_PFT_GENERICCROPS, MAX_PFT_MANAGEDCROPS
  python/ctsm/site_and_regional/plumber2_surf_wrapper.py:31:from ctsm.pft_utils import MAX_PFT_MANAGEDCROPS, is_valid_pft

  $ git log --format="%h %ad %an %s" --date=short -3 -- python/ctsm/pft_utils.py
  b7f7af386 2025-06-20 Sam Rabin plumber2_surf_wrapper: Better is_valid_pft() check.
  8ca6e4556 2025-06-20 Sam Rabin Rename and replace some PFT number constants for clarity.
  602fe61fb 2025-06-20 Sam Rabin Move Python constants for PFT numbers to pft_utils.py.
  ```
- **My findings:** Part of the issue is still true and part is not. There is still no `MONTHS_PER_YEAR`, and the number of months is a literal repeated three times in one module. The PFT constants the issue asked for no longer need a new file: Sam Rabin moved them into `ctsm/pft_utils.py` on 2025-06-20 under the names `MAX_NAT_PFT` and `MAX_PFT_MANAGEDCROPS`, not NATPFT and MXPFT. ekluzek's 2022 review of PR #1461 says the shared-file idea was meant to let `subset_data.py` use the single-point constants ("...or #1621 also done"), and `subset_data.py` now imports them from `pft_utils.py`. By reading the code I also noticed two small leftovers in `single_point_case.py` (a docstring with literal 78 and 16 on line 59, and a `--dompft` error on line 223 that says "between 1 and" though 0 is allowed); I did not test either. So the claim I posted ("switch the existing python modules that define those values") describes more work than exists. I asked ekluzek about scope and location on #1621 (https://github.com/ESCOMP/CTSM/issues/1621#issuecomment-6695341126) and have not had an answer yet.

**Toolkit**

- Tool: repro-check, with the wild scope.
- What it produced: two runs on my claim draft and repro report. Run 1 rejected on evidence-based (my report asserted the import list, commit hashes and "became #1621" without quoting output) and on comms. After I added quoted output and ekluzek's comment, run 2 passed environment, steps, behavior and evidence, and rejected only on comms.
- Difficulties: it reads `claim-draft.md`, which no longer matched the claim I posted, and the comms failure rested partly on an AI-disclosure requirement that I (and Claude) read into PR #4286 too broadly. #4286 asks for disclosure in the PR template and issue forms, not in comments on an existing issue, so I judged that part too strict. The claim draft itself is still out of date, because it describes switching modules that define NATPFT and MXPFT, which do not exist.
- What changed: I rewrote the report so every claim has a command and its output next to it. I chose to move on without updating `claim-draft.md`, so the grader has not passed; I will put the AI disclosure in my PR description, where #4286 asks for it.

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
