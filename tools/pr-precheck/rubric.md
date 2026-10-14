# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diff-matches-plan | The diff's changed files and hunks, read against the plan's in-scope statement, files-to-touch list, and any deviation notes. | Every changed file and behavior in the diff falls inside the plan plus its recorded deviation notes, and nothing the plan committed to is missing from the diff, including any test the plan commits to adding (a test file in its Files list, or a plan step that says to add a test for a named case): each must be in the diff or its omission disclosed. Manual control runs the test plan names are graded under tests-observable, not here. A change the plan did not name passes only if a deviation note records it and says why. A planned piece that is absent passes only if the plan's deviations or the description discloses the omission (an honestly disclosed shortfall is not drift). Fails if the diff silently does more than the plan (an unplanned file or behavior change with no note) or silently does less (a planned change missing with no disclosure). | required |
| description-matches-diff | The PR description's Summary and Changes sections, read against the diff. | Each claim in the description (what changed, what was fixed, "no other changes") is something the diff actually shows, and each substantive change in the diff is described. Fails if the description claims a change, fix, or fidelity to the plan that the diff contradicts or does not contain, or if it leaves a substantive diff change unmentioned. A loosely worded claim the diff substantially supports (for example a test described as several cases when one test covers them) passes. | required |
| fix-addresses-issue | The diff's core change, read against the issue's reported behavior and the plan's stated cause. | The change acts on the cause the plan names and answers the behavior the issue reports; it is not a workaround that only hides the symptom, and it is not an unrelated change. Fails if the core change would leave the reported behavior in place or targets something other than the plan's cause. | required |
| tests-observable | The test evidence (the repro re-run before and after, and the output of the repo's own checks named in the PR template), read against the plan's test plan. | The evidence shows an observable before/after difference from the plan's repro (specific output, value, or behavior that differs and matches the plan's expected result), and the repo's own checks (the commands the repo's template or the package names) were run with a stated result. A check that fails or stops (for example "no tests ran") passes when the result is reported honestly with the reason. Fails if the evidence is only "it works" or "tests pass", could pass whether or not the bug were fixed, omits the before or the after, shows a different scenario than the plan's repro, states no result for the repo's checks, or reports a result the pasted output contradicts. The before and after must quote concrete observed output (the error text, value, or rows the run produced), whether as a command transcript or as annotated lines in one; a vague note such as "works now" or "colors work" with no quoted output fails. Once that decisive before/after is shown, a control run the plan names, and the result of the repo's test command, count when the package states a concrete result for them (an exit code, a quoted line, or "N tests passed"), even without a full transcript; they fail if the result is missing, vague, or contradicted by the pasted output. Claims in the description's Testing section must be backed by the pasted output. | required |
| diff-reviewable | The diff itself: every hunk, including whitespace and formatting changes, read against the change the plan describes. | A reviewer can see the change: no debug lines (print or console statements, leftover logging), no commented-out code, no unrelated formatting or reformatting hunks, no unrelated files, and no generated or planning files (plan.md, comment.md, pr_draft.md, test_evidence.md) committed. Fails if any such debris appears, or if unrelated hunks are large enough to bury the real change. | required |
| standards-met | The description read against the repo-facts or the real repo's PR template, `docs/CONTRIBUTING.md`, and any stated AI-use policy; the branch name and PR title read against the repo's stated conventions. | Every section the template asks for is filled with real content (not left as template text), the issue is named (for example `Closes #N`), the Testing boxes ticked are true (the CI box may stay unticked), and the AI-use disclosure the repo requires is present in the description in the writer's own words. Any file the repo requires alongside a change (for example a changelog entry) is present in the diff. Any other condition the repo states (branch name type prefix, title convention) is met. Fails if a required section is empty or placeholder text, a required file such as a changelog entry is missing from the diff, the issue is not named, a ticked box is contradicted by the evidence, or the repo's stated disclosure ask is ignored. Silence in the repo's policy requires nothing. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept only if every required check grades pass; this rubric has no preferred checks. If any required check grades fail or unclear, the verdict is reject. `unclear` counts as `fail`: a PR whose claims cannot be verified from the package is not ready to submit. A shortfall that the description or plan honestly discloses does not by itself fail a check (see diff-matches-plan and tests-observable); an undisclosed one does.
