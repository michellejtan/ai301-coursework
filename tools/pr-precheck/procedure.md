# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->
1. Read the scope first (live mode only): `scope.md`, then `voice-guide.md`. Stop here if the scope refuses (see SKILL.md). Eval mode skips both.
2. Read the issue second (eval: the bundle's issue context; live: the issue body and thread). Note the symptom it reports, the trigger, and any maintainer signals (assignee, stated preferences, a required template).
3. Read the repo's standards third (eval: the bundle's repo-facts block; live: the PR template and `docs/CONTRIBUTING.md`). Note every section the template asks for, any file the repo requires with a change (such as a changelog entry), the branch and title conventions, and the AI-use disclosure policy.
4. Read the plan fourth, whole, before opening the diff. Note its stated cause, in-scope and not-in-scope lines, the exact list of files it names, its test plan (the fix test, any control run, any nested or edge cases), and its Deviations section if it has one. Read it before the diff so the diff is judged against what was promised, not the other way around.
5. Read the diff fifth, every hunk (live: `git diff main...HEAD`). Note each changed file, what each hunk changes, and anything that looks like debris (debug lines, commented-out code, formatting-only hunks, unrelated files, planning files).
6. Read the test evidence sixth (eval: the bundle's test-evidence block; live: `test_evidence.md`). Note which commands were run and whether each result quotes concrete output or is only a vague note.
7. Read the PR title and description last (live: `pr_draft.md`). Read them last so their claims are held against everything already read. Note each claim in Summary, Changes, and Testing, the issue reference, each ticked box, and the AI-use disclosure.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->
1. diff-matches-plan: list every file the diff changes next to every file the plan names. Record each changed file the plan does not name, and whether a deviation note covers it. Record each behavior the diff changes beyond the plan. List every test the plan's test plan names (the issue's input, any control, any nested or edge cases) and record whether the diff contains a test for each. Record each planned piece missing from the diff and whether the plan or description discloses it.
2. description-matches-diff: copy each claim from Summary, Changes, and any "no other changes" or "implements the plan" statement. Beside each, record the diff hunk that shows it, or "no hunk". Record each substantive diff change the description never mentions.
3. fix-addresses-issue: copy the issue's reported behavior and the plan's stated cause. Record what the diff's core change does and whether it acts on that cause or only hides the symptom.
4. tests-observable: copy the plan's test plan and its expected result. Record, for the before run, the after run, each control run, and each repo check the template lists (`make test-unit`, `make test-integration`, `make lint`, `make typecheck`), whether it quotes concrete observed output or only a vague note, and what the output shows. Record each Testing claim in the description that has no quoted output or stated result behind it.
5. diff-reviewable: from the diff, record each hunk that is debug output, commented-out code, formatting-only, in an unrelated file, or a planning file (plan.md, comment.md, pr_draft.md, test_evidence.md). Record roughly how much of the diff is unrelated against the real change.
6. standards-met: list each section the template asks for and record whether it holds real content or template text. Record the issue reference, each ticked box and whether the evidence supports it, the AI-use disclosure text, any file the repo requires with a change and whether the diff has it, and the branch name and title against the repo's conventions. A CI box left unticked is not a gap.
7. In eval mode use only the bundle text. Where the evidence guide names a location the package lacks, record "absent" for that check.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
1. Run the checks in the rubric's table order.
2. Grade each check against its pass condition using only the evidence recorded in the gathering step. Record one quote or fact for the grade.
3. If the evidence a check needs is absent from the package (for example, no test evidence at all, or no plan to compare against), grade it `unclear` and write "absent: <what is missing>" as the evidence. Do not infer the missing evidence from other parts of the package.
4. If the pass condition has several parts, every part must hold for a pass. One part failing is a `fail`, not `unclear`.
5. A shortfall the plan's Deviations or the description honestly discloses is not drift or a gap: grade the check on whether the disclosure is accurate. An undisclosed shortfall fails.
6. A pre-existing option, function, or file the diff only uses is not an addition; only grade what the diff changes.
7. A check may be graded from its recorded evidence without re-reading the whole package, except diff-matches-plan, description-matches-diff, and tests-observable, which always re-read the diff (and, for tests-observable, the pasted output itself) before grading.
8. Grade the thing itself, not its shape: do not pass or fail a check for headings, length, or polish.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->
1. List every check's grade in the rubric's table order.
2. Apply the rubric's verdict rule: accept only if every required check is `pass`. Any `fail` or `unclear` on a required check gives reject. `unclear` is counted as `fail`.
3. Output `accept` or `reject` only. There is no third verdict.
4. In the output, quote the deciding evidence for every failed or unclear check; when more than one failed, lead the summary with the first failing required check in rubric order as the deciding check. If the verdict is accept, quote the evidence for the weakest passing check.
5. In live mode, add any voice-guide rule the PR title or description breaks to the summary, quoting the rule and the offending text. It never changes a grade. Note any gap where this procedure was silent.
6. End with the JSON block, valid and last, with `item` set to the PR URL (live) or the bundle id (eval).
