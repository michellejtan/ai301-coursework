# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

- Where it lives: in an eval bundle, the "Plan context" section (the plan's steps, its "Not in scope" line, its "Files" list, and its test plan; a deviation note, if any, sits there too), read against "Candidate PR", "Diff" (the changed files and hunks) and "Description" (its Summary and Changes claims). In live mode: `plan.md` and its `## Deviations` section, read against the output of `git diff main...HEAD` and the description in `pr_draft.md`.
- What good looks like: every changed file and behavior in the diff is inside the plan's named files and steps or a deviation note, and every test the plan commits to adding has a file or hunk in the diff. Silent drift is an unplanned file or behavior change with no note, a planned piece missing with no disclosure, or a description that claims "implements the plan exactly" or "no other changes" that the diff contradicts. A deviation that is recorded and explained, or a shortfall the description discloses, is honest and still ties the diff to the plan.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

- Where it lives: in an eval bundle, the "Test evidence" section under "Candidate PR", read against the test plan in "Plan context" and the repro evidence quoted there. In live mode: `test_evidence.md`, read against the test plan in `plan.md`, plus the four checks the repo's PR template lists (`make test-unit`, `make test-integration`, `make lint`, `make typecheck`) and the Testing section of `pr_draft.md`.
- What good looks like: the repro command is shown with real pasted output for the before and the after, and the after differs from the before in the way the plan's expected result says. Any control run the plan names, and each repo check, has a concrete stated result (in your own PR, paste the output). A check that fails or stops ("no tests ran") is fine when the reason is stated. A vague note such as "works now" or "tests pass" with no quoted output or count is a claim, not evidence.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

- Where it lives: in an eval bundle, the "Diff" and "Commits" sections under "Candidate PR". In live mode: the output of `git diff main...HEAD` and `git diff main...HEAD --stat` for the file list, plus `git log main..HEAD` for the commits.
- What good looks like: a reviewer can see the fix in the diff and every hunk belongs to it. The debris tells are print or console debug lines, commented-out code, formatting-only or whitespace hunks, edits to files the change doesn't need, and planning files (`plan.md`, `comment.md`, `pr_draft.md`, `test_evidence.md`) committed to the branch. A tiny diff with one removed line, like calib-01's, is reviewable; a large reformat that buries a small fix is not.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

- Where it lives: in an eval bundle, the "Repo facts" block (its PR template sections, contribution asks, stated policy, and AI-use policy) and the "Thread highlights", read against the PR's "Title" and "Description". In live mode: the PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and `docs/CONTRIBUTING.md` in the Path Review repo, read against `pr_draft.md` and the branch name; any file the repo requires with a change (for example a changelog entry) is checked in the diff.
- What good looks like: every section the template asks for holds real content, the issue is named (for example `Closes #N`), each ticked box is backed by the evidence (the CI box may stay unticked), and any AI-use disclosure the repo asks for is present in the writer's own words. Any required file, such as a changelog entry, is in the diff, and the branch name and title follow the repo's convention. When the repo states no template or policy (as in calib-01: "no PR template", "no stated AI policy"), nothing extra is required, and a short description that references the issue and stays small is compliant. An empty section, leftover template text, a missing disclosure, or a missing required file is a visibly ignored ask.
