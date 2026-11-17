# Checking an Old Issue Before Building: My CTSM Constants PR, and the Gate I Patched to Ship It

## Overview

CTSM (the Community Terrestrial Systems Model) is a large open-source land-surface model from NCAR, with a Python toolchain. Issue [#1621](https://github.com/ESCOMP/CTSM/issues/1621), opened in 2022, asked for a shared Python file of constants (NATPFT, MXPFT, MONTHS_PER_YEAR) so modules stop repeating the same numbers. I claimed it, found that most of it had already been done, and opened [PR #4310](https://github.com/ESCOMP/CTSM/pull/4310) for the part still missing: a `MONTHS_PER_YEAR` constant that replaces three hard-coded `range(1, 13)` loops. The PR is open and has had no review or comment yet, so today it is "opened a fix," not "fixed." The tool I also feature is my **ship-gate**, a pre-PR check. I wrote its manifest (CTSM's three CI checks, each with a full conda path) and patched its issue fetcher so it could read CTSM's issue thread.

## What happened

**1. The issue was mostly stale.** I claimed #1621 on 2026-11-01, and maintainer ekluzek replied within about two hours, asking me to base my work on `b4b-dev`. I searched the code for the names mentioned in the issue but couldn't find them. At first, I thought nobody had worked on them yet. Then I tried a different way. I searched for the numbers and looked at the code's history. `git log` on `pft_utils.py` showed that Sam Rabin had moved and renamed the PFT constants on 2025-06-20. Only `MONTHS_PER_YEAR` was actually missing:

```
$ grep -rn "MONTHS_PER_YEAR" --include="*.py" . ; echo "exit=$?"
exit=1
$ grep -rn "range(1, 13)" --include="*.py" python/ctsm | grep -v /test/
python/ctsm/cplhist/cplhist_monthly_clim.py:130: ... for month in range(1, 13)]
python/ctsm/cplhist/cplhist_monthly_clim.py:751:            for month in range(1, 13)
python/ctsm/cplhist/cplhist_monthly_clim.py:833: ... for month in range(1, 13)]
```

*(This output is the real reproduction from my clone of `b4b-dev`; it shows the constant is absent and the literal is repeated three times.)*

**2. I changed my plan because of that finding.** My claim comment had promised a new module holding all three constants. After the history check I dropped that. I posted a question on #1621 describing what I found and asking whether the job was now just `MONTHS_PER_YEAR`. I kept the plan small: a new `python/ctsm/constants.py`, the three replacements, and a separate, droppable commit for two leftovers in `single_point_case.py` (a docstring with literal "78 pft, else 16 pft" and a `--dompft` error that said "between 1 and" although 0 is allowed). ekluzek has not answered that question in the ten days since, so I went ahead with my proposed file location and said so in the PR.

**3. Test first, and one test that was honest about not failing.** I wrote each test before the change and watched it fail:

```
ImportError: cannot import name 'constants' from 'ctsm'
"values for --dompft should be between 0 and" does not match
"values for --dompft should be between 1 and 78."
```

A third planned test, that `NOLEAP_DAYS` has `MONTHS_PER_YEAR` entries, passed both before and after. I kept it as a consistency guard and said so in the PR instead of calling it a before/after test. The repo's checks then gave 680 unit tests passing (677 before plus my 3), black unchanged, and pylint 10.00/10. Getting there took a day: conda was killed for lack of memory on my 3.8 GB WSL machine, and 35 tests failed because Git LFS was not installed, so the test data files were text pointers.

**4. The ship-gate stopped me, and I fixed the gate.** My gate runs the manifest checks and then grades the PR against the plan and issue. Its first run passed the three repo checks but could not grade whether the fix addressed the issue:

```
fix-addresses-issue [unclear]: absent: the #1621 thread could not be fetched
(GraphQL Projects-classic error), so the issue's reported behavior can't be
compared with the diff's core change.
```

The cause was my `gh` 2.45.0 asking GitHub for a field that no longer exists on CTSM. I patched `fetch_issue()` in my installed copy of the gate (keeping a backup) to request explicit `--json` fields, falling back to the original call if that fails:

```python
fields = "title,body,state,author,assignees,labels,createdAt,url,comments"
res = sh(["gh", "issue", "view", url, "--json", fields], timeout=GH_TIMEOUT_S)
```

This was a change to the course's tool, not to my own rubric. After the patch, the same check came back `[pass]`: "#1621 asks for a shared constants module with MONTHS_PER_YEAR; the diff adds ctsm/constants.py and uses it at the three literals." All six pr-precheck checks and the three repo checks passed. The gate also called "Fixes to #1621" the weakest pass, so I changed it to "Fixes #1621" before posting. I did not re-run the gate after that edit and my AI-disclosure rewrite.

**5. How it landed.** CTSM's AI rules (PR #4286) say LLMs must not submit or edit issues or PRs, so Claude drafted and I reviewed the full diff, committed, and opened the PR myself in the browser on 2026-11-09. The PR description discloses Claude's help. The results that landed are concrete but modest: ekluzek accepted my claim quickly, and my gate's pass is what let me open a PR whose description matches its diff. My PR monitor's first run on 2026-11-09 reported "1 check pending," but GitHub showed three workflows as `action_required`, meaning a maintainer must approve a first-time contributor's CI run. As of 2026-11-16 the PR is open with zero comments and zero reviews, and CI has not run.

## Limitations and what's next

The PR has not been reviewed. The file location (`python/ctsm/constants.py`) is my proposal. No maintainer answer on it. The "leftovers" commit is only loosely what the issue asked for, which is why it is separate. I did not run all the Python system tests. Five tests were skipped because NCO was not installed on my computer. This means I only used unit tests to `cplhist_monthly_clim.py`.

My tools have limits too. The gate's pass is evidence I gathered myself, not something that blocked a bad PR, since I opened the PR outside Claude Code and its hook never fired automatic. My patch lives only on my computer, and the monitor still misreads `action_required` as "pending."

My next steps are to follow up on the PR and improve my tools. My playbook says to send nudge after 14 days. That date is November 23, 2026. If nobody replies for another six weeks, I plan to close the PR. I will write the nudge myselfthat it needs a maintainer's approval before postingv via browser. For the monitor, I will add a rule for CI runs awaiting approval, so it says "needs maintainer approval" instead of "pending."