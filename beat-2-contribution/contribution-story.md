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
**Pull Request:** https://github.com/ESCOMP/CTSM/pull/4310

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

**Unit 7: Installed the ship-gate, wrote a manifest of CTSM's unit tests, black and pylint, and patched the gate's issue fetch for CTSM**

I installed the ship-gate (its hook test gave the expected stops on `gh pr create --help`) and wrote a manifest of CTSM's three CI checks (unit tests, black, pylint), each with the full conda path so it runs in a fresh terminal. The gate stopped twice before it passed: first because I had no local `b4b-dev` branch to compare against, which I fixed by creating one that tracks upstream, and then in pr-precheck, where `fix-addresses-issue` was `unclear` because the gate could not fetch the #1621 thread; `gh issue view` fails on CTSM with my `gh` 2.45.0, which asks GitHub for a removed Projects (classic) field. I patched `fetch_issue()` in my own installed copy of the course's `check_gate.py` (a local change to the course's tool, with a backup kept) to use explicit `--json` fields and fall back to the original code, and I tested that it returns the issue body and all three comments. After the patch the gate passed the three repo checks and all six pr-precheck checks, with my issue line ("Fixes to #1621") as the weakest pass, so I changed it to "Fixes #1621" and updated on my AI disclosure before posting, without re-running the gate. I opened the PR myself in the browser, not through Claude Code, because ekluzek pointed me to CTSM's PR #4286, which says LLMs must not submit PRs.

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

CTSM#1621 asks for a small shared Python file of constants (it names NATPFT, MXPFT and MONTHS_PER_YEAR) so Python modules stop repeating the same numbers. Nothing crashes; it is a code-health issue where the same value is written in several places and can drift apart. When I checked `b4b-dev`, most of it was already done: the PFT numbers live in `python/ctsm/pft_utils.py`. What is still missing is a constant for the number of months in a year.

**Expected Behavior**

Shared numbers should be defined once under a clear name and imported where they are used, including in comments and error messages, so that changing the value in one place changes it everywhere.

**Current Behavior**

There is no `MONTHS_PER_YEAR`. The loop `range(1, 13)` is written three times in `python/ctsm/cplhist/cplhist_monthly_clim.py` (lines 130, 751, 833). Two spots in `single_point_case.py` still use the plain PFT numbers: the docstring on line 59 says "78 pft, else 16 pft", and the `--dompft` error on line 223 says "between 1 and ..." although 0 is allowed.

**Affected Components**

`python/ctsm/cplhist/cplhist_monthly_clim.py` (the three month ranges), `python/ctsm/site_and_regional/single_point_case.py` (the docstring and error message), `python/ctsm/pft_utils.py` (already has the PFT constants, not changing it), and the tests in `python/ctsm/test/` (`test_unit_cplhist_monthly_clim.py`, `test_unit_singlept_data.py`).

**Toolkit**

- Tool: Claude Code reading the clone, `git log`, and the issue and PR threads through `gh`, guided by my `CLAUDE.local.md`.
- What it produced: the finding that PFT constants were already moved to `pft_utils.py` in June 2025, the three `range(1, 13)` literals, and the 2022 PR #1461 comment that explains why #1621 was opened.
- Difficulties: the issue was opened on 2022-01-29 and names three constants (NATPFT, MXPFT, MONTHS_PER_YEAR), but I am reading the code now in November 2026, almost five years later, and two of those names no longer exist. My first search for them found nothing useful: it matched only a test variable (`natpft = np.arange(0, 15, 1)`), and my first command also failed because zsh tried to expand the unquoted `--include=*.py` as a file glob. A broader, case-insensitive search then found `natpft` many times, but only as a netCDF dimension name in `modify_fsurdat.py`, `fsurdat_modifier.py` and `single_point_case.py` (for example `max(self.file.natpft)`), which is data from a file and not a constant. A search of the whole repo for NATPFT, MXPFT and MONTHS_PER_YEAR found nothing at all, so for a while I thought none of the issue had been started. What broke that loop was two things. I searched for the literal numbers instead of the names (`78`, `16`, `15`), which turned up `MAX_PFT_MANAGEDCROPS = 78` in `python/ctsm/pft_utils.py`. Then I read PR #1461, where the constants first appeared under the underscored names `NAT_PFT`, `MAX_PFT` and `FIRST_MONTH`/`LAST_MONTH`, and re-ran the search with those names. `git log` on `pft_utils.py` and commit 602fe61fb showed that Sam Rabin moved them there on 2025-06-20 and, in the next commit, renamed `NAT_PFT=15` to `MAX_NAT_PFT=14`, `NUM_PFT=17` to `MAX_PFT_GENERICCROPS=16`, and `MAX_PFT` to `MAX_PFT_MANAGEDCROPS`. The old `NAT_PFT` was a count (15) and the new `MAX_NAT_PFT` is a highest index (14), so even the meaning changed, not just the spelling. Only then did I understand that the PFT half of the issue was done, and that the one name with no rename or replacement, `MONTHS_PER_YEAR`, was the real remaining work. The lesson is that an old issue's names are a description of an idea, not a search string: search for the values and the history, not only the names.
- What changed: I stopped planning a new module that would duplicate `pft_utils.py` and asked ekluzek about scope on the issue. I did not wait for his answer to write the plan.

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

This is a code-health issue, not a crash. Most of what CTSM#1621 asks for is already done: the PFT constants live in `python/ctsm/pft_utils.py` (added 2025-06-20) and four source modules import them (`subset_data.py`, `toolchain/gen_mksurfdata_namelist.py`, `site_and_regional/single_point_case.py` and `site_and_regional/plumber2_surf_wrapper.py`). What is still true is that the number of months in a year has no named constant. It is written as the literal `range(1, 13)` three times in `python/ctsm/cplhist/cplhist_monthly_clim.py`: in `year_months()` (line 130), in the averaging step (line 751) and in the step that puts the twelve monthly files together (line 833). `grep -rn MONTHS_PER_YEAR` finds nothing in the repo. I read the three call sites and each one loops over calendar months 1 to 12, but I have not run anything that depends on that; the existing unit tests for `year_months` and the climatology code are my check.

Two small leftovers from the earlier PFT work are in `python/ctsm/site_and_regional/single_point_case.py`, found by reading the code and not tested: the docstring on line 59 says "if crop 78 pft, else 16 pft" (literal numbers that go stale if `MAX_PFT_MANAGEDCROPS` or `MAX_PFT_GENERICCROPS` change), and the `--dompft` error on line 223 says "between 1 and ..." although the check on line 222 allows 0 (`MIN_PFT = 0` already exists in `pft_utils.py`).

**Proposed Solution**

Add one small module, `python/ctsm/constants.py`, holding `MONTHS_PER_YEAR: Final[int] = 12`, and use it in `cplhist_monthly_clim.py` instead of the three `range(1, 13)` literals. Then, as a separate commit, make the two leftovers use the constants that already exist. The file location is my proposal, which I asked ekluzek about on #1621 and have not had an answer to; if he wants it somewhere else I will move it.

What I am not changing: `pft_utils.py` and its constants, the repeated `"NETCDF4_CLASSIC"` string, `NOLEAP_DAYS` (I only add a test that its length equals `MONTHS_PER_YEAR`), the `# 12 months` comments in `modify_fsurdat.py`, `end_month = 12` in `run_tower.py` (a run setting, not a calendar constant), and any `range(1, 13)` in test files. Anything else I find goes in its own issue or PR. If ekluzek says the leftovers are out of scope, I drop commit 3.

**Implementation Plan**

1. Create `python/ctsm/constants.py` with `MONTHS_PER_YEAR`, and a new `python/ctsm/test/test_unit_constants.py` that asserts it equals 12 (this test fails before the change, with an ImportError).
2. In `python/ctsm/cplhist/cplhist_monthly_clim.py`, import `MONTHS_PER_YEAR` and replace the three `range(1, 13)` with `range(1, MONTHS_PER_YEAR + 1)`. Add a test in `test_unit_cplhist_monthly_clim.py` that `len(mclim.NOLEAP_DAYS) == MONTHS_PER_YEAR`.
3. In `single_point_case.py`, reword the line 59 docstring to name `MAX_PFT_MANAGEDCROPS` and `MAX_PFT_GENERICCROPS`, and change the line 223 error to use `MIN_PFT` ("between {MIN_PFT} and ..."). Add a unit test in `test_unit_singlept_data.py` that the error text says "between 0 and" (fails before the change).
4. Run the three checks in my ship manifest (unit tests, black, pylint) and save before/after output in `test_evidence.md`.

Deviations: none yet.

**Toolkit**

- Tool: plan-check, with the wild scope, run on `plan.md` and `plan-comment.md` in my CTSM clone.
- What it produced: one run, verdict accept, with all six checks passing (diagnosis-grounded, scope-bounded, executable-by-stranger, test-plan-observable, honest-about-unknowns, comms-thread-aware). It named test-plan-observable as the weakest pass, because the plan's tests fail before the change but the plan does not re-run my repro greps with an expected after-output. It reported no voice-guide rule broken.
- Difficulties: plan-check expects the repro evidence to be my posted repro comment, but this unit says not to post the repro, so there was nothing posted to read it against and it graded the plan against what plan.md says about the repro. My procedure.md is silent about that case. The leftovers commit (the docstring and error message in `single_point_case.py`) is only loosely the issue's ask and ekluzek has not confirmed it, so the scope pass depends on keeping it a separate commit I can drop.
- What changed: I have not changed the plan to add the repro re-run it flagged yet, and I plan to add it to `test_evidence.md`.

---

## Testing Strategy

I re-ran my reproduction steps on the unchanged branch and again after the fix, and ran the repo's own checks (`run_ctsm_py_tests`, black, pylint). Before the fix, `grep -rn "MONTHS_PER_YEAR" --include="*.py" .` printed nothing (`exit=1`) and `grep -rn "range(1, 13)" --include="*.py" python/ctsm | grep -v /test/` printed three lines in `cplhist_monthly_clim.py` (130, 751, 833). After the fix the first grep finds `MONTHS_PER_YEAR` in `constants.py` and at the three places in `cplhist_monthly_clim.py`, and the second grep prints nothing (`exit=1`).

Two new unit tests fail before the change and pass after: `test_unit_constants.py` fails with `ImportError: cannot import name 'constants' from 'ctsm'`, and `test_check_dom_pft_message_lower_bound` fails with `"values for --dompft should be between 0 and" does not match "values for --dompft should be between 1 and 78."`. A third test, `test_noleapDaysMatchMonthsPerYear`, passes before and after (demonstrates that an existing safeguard continues to work); it only guards against the constant and `NOLEAP_DAYS` drifting apart.

The repo's checks, from my ship manifest, in the `ctsm_pylib` conda environment: `./run_ctsm_py_tests -u` gives 680 passed (677 before my changes plus my 3), `make -C python black` leaves 182 files unchanged, and `make -C python lint` rates 10.00/10. I did not get a python system-test result: CI runs only the unit tests, and when I tried the one relevant file (`test_sys_aero_1850_monthly_clim.py`) all 5 tests were skipped because NCO (`ncra`, `ncrcat`, `ncatted`) is not installed on my machine. The full output is in `test_evidence.md` on my computer, and the key lines are in my PR description.

**Toolkit**

- Tool: the repo's own checks (`run_ctsm_py_tests`, black, pylint) run from my ship manifest, with Claude Code running them and capturing the output.
- What it produced: before and after output for the reproduction greps, two tests that fail first for the right reason, and a passing run of all three checks (680 tests, black clean, pylint 10.00/10).
- Difficulties: the first unit-test run had 35 failures that were not my code: the test input `.nc` files were Git LFS pointer files because `git-lfs` was not installed, so xarray could not open them. Creating the conda environment was also killed for running out of memory on my 3.8 GB WSL machine, and a later attempt left a half-built environment that I had to rebuild.
- What changed: I installed `git-lfs` and ran `git lfs pull`, then rebuilt the environment with mamba (`./py_env_create -m -y -o`), and recorded both in my `CLAUDE.local.md`. I also noted in the evidence that one new test is a consistency guard and does not fail before the change.

---

## Implementation Notes

**2026-11-07**

Set up the CTSM test environment so I could run the project's checks. The first `conda env create` was killed while solving ("Killed" with no message); `dmesg` showed the kernel's out-of-memory killer, because WSL has 3.8 GB of RAM. A second attempt with mamba left a half-built environment (black, pylint, netCDF4 and xarray were missing), so I rebuilt it with `./py_env_create -m -y -o`. The first unit-test run then had 35 failures. The cause was not my code: 54 of the 55 test input `.nc` files were Git LFS pointer files because `git-lfs` was not installed. After `git lfs pull`, all 677 tests passed. Wrote the ship manifest (unit tests, black, pylint, each checked in a fresh terminal) and the plan, which plan-check accepted.

**2026-11-08**

Fast-forwarded `constants-module` to upstream `b4b-dev` (0efa002a5, 31 commits ahead) and re-checked that the lines in my plan had not moved. ekluzek had not answered my question about where `MONTHS_PER_YEAR` should live, so I went ahead with my proposed location, `python/ctsm/constants.py`, and said so in the plan. Built it as three commits, writing each test first and running it to see it fail: the module and its test, the three `range(1, 13)` replacements, and the docstring and `--dompft` error fix, kept separate so it can be dropped. black reformatted one long line in `year_months()`; I used `range(1, MONTHS_PER_YEAR + 1)` as planned. One planned test turned out not to fail before the change (`NOLEAP_DAYS` has 12 entries either way), so I kept it as a consistency guard and said so in `test_evidence.md` instead of calling it a before/after test. Because of CTSM's AI rule (PR #4286), I decided that I commit and open the PR myself and review the whole diff first; the three commits Claude made were undone with a soft reset so I could re-make them. No deviation from the plan.

**Toolkit**

- Tool: Claude Code with `CLAUDE.local.md`, plus plain git for the commits.
- What it produced: the three changes and their tests, test-first with the failures captured, and the before and after output in `test_evidence.md`.
- Difficulties: the environment setup (out-of-memory kills, a half-built environment, and git-lfs pointer files) cost most of a day before any code changed, and none of it was in CONTRIBUTING.md. The repo's AI rule also conflicts with the course's step that has Claude Code open the PR.
- What changed: I wrote the environment fixes into `CLAUDE.local.md` so the next session starts with them, and I follow the repo's rule, not the course's, by opening the PR myself instead of through Claude Code.

---

## Pull Request

**PR Link:** https://github.com/ESCOMP/CTSM/pull/4310

**PR Description:** The PR is "Add MONTHS_PER_YEAR constant and use it in cplhist_monthly_clim", from `michellejtan:constants-module` into `ESCOMP/CTSM:b4b-dev`, with three commits and six files (+86, -6). It adds `python/ctsm/constants.py` with `MONTHS_PER_YEAR`, replaces the three `range(1, 13)` month loops in `cplhist_monthly_clim.py` with it, and, in a separate commit that is easy to drop, makes a docstring and the `--dompft` error in `single_point_case.py` use the existing PFT constants (the error now says "between 0 and 78"). The description says what I did not change (`pft_utils.py`, the `"NETCDF4_CLASSIC"` string, `NOLEAP_DAYS`, `run_tower.py`), says I asked on #1621 where `MONTHS_PER_YEAR` should live and got no answer, and quotes the before and after greps. It lists two new tests that fail first and a third consistency test that does not, 680 unit tests passing, black and pylint clean, and the skipped system tests with the reason (NCO is not installed). Its AI disclosure says Claude Code helped explore the code and wrote the first version of the code, and tests, and that I review the diff and ran the checks CI runs myself. It says "Fixes #1621".

**Maintainer Feedback:**

- 2026-11-09: none yet. I opened the PR on this date. When I checked, nobody had commented or been asked to review, and GitHub showed no CI runs for the commit yet, so I do not know whether CI is waiting for a maintainer to approve it.

**Status:** Awaiting review

**Toolkit**

- Tool: the ship-gate (my manifest checks plus my pr-precheck), run by hand before I opened the PR.
- What it produced: a pass on the three repo checks (unit tests 68s, black 13s, pylint 280s) and on all six pr-precheck checks (diff-matches-plan, description-matches-diff, fix-addresses-issue, tests-observable, diff-reviewable, standards-met), with the issue-line wording as the weakest pass.
- Difficulties: its first run stopped because `gh issue view` fails on CTSM, and its normal path has Claude Code open the PR, which conflicts with CTSM's PR #4286 ("LLMs must not submit ... PRs").
- What changed: I patched the gate's `fetch_issue()` in my own copy and opened the PR myself in the browser, so the gate's hook did not fire on the PR. The gate's pass is my evidence, not a hook that stopped anything.

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
