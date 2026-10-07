# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->
1. Read the issue context first (live: the issue body and thread). Note the symptom it reports, the trigger, any maintainer signals (who is assigned, stated preferences, a requested template), and whether a prior plan already exists.
2. Read the repro evidence second (eval: the repro-evidence block; live: the student's posted repro comment, or the house repro pack as quoted in the drafts). Note the exact command, the quoted output or error, and what behavior it pins down. Read it before the plan so you know what a correct cause must explain.
3. Read the repo-facts block third (live: scope.md plus the repo's CONTRIBUTING and AI policy). Note stated templates, contribution asks, and the AI-use policy.
4. Read the candidate plan fourth, whole, before grading. Note its stated cause, in-scope and not-in-scope lines, files touched, approach, test plan, risks and unknowns, and whether it ends with a Deviations heading.
5. Read the candidate plan comment last. Note what it says about cause, scope, and approach, and what it says about the thread.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->
1. diagnosis-grounded: copy the plan's stated cause and the repro evidence line (quoted output or error) it should explain. Record whether the plan quotes that evidence itself.
2. scope-bounded: copy the plan's in-scope statement, its not-in-scope line, and every file or area named. Record anything named that the issue's ask does not need.
3. executable-by-stranger: copy the files-to-touch list and the approach. For each file or function named, check it against the repo-facts block (eval) or the repo (live) and record whether it exists (live) or whether the package contradicts it (eval; the bundle has no file listing, so a plausible but unverifiable path is not a failure).
4. test-plan-observable: copy the test plan and the repro steps. Record whether the plan re-runs those steps and what expected result it names, next to the repro's quoted "before."
5. honest-about-unknowns: copy the risks and unknowns text (if the plan has none, record that and note whether its cause is directly supported by the repro). Record any claim of certainty in the diagnosis or approach that the repro evidence does not demonstrate, and any promised outcome.
6. comms-thread-aware: copy the plan comment and the thread's maintainer signals and the repo's stated template, ask, and AI policy. Record whether the comment mentions a detail from this thread and whether it restates the plan.
7. Use only the package text as evidence in eval mode. Where the evidence guide names a location the package lacks, record "absent" for that check.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
1. Run the checks in the rubric's table order.
2. Grade each check against its pass condition using only the evidence recorded in the gathering step. Record one quote or fact for the grade.
3. If the evidence a check needs is absent from the package (for example, no repro evidence is quoted at all), grade it `unclear` and write "absent: <what is missing>" as the evidence. Do not infer the missing evidence from other parts of the package.
4. If the pass condition has several parts, every part must hold for a pass. One part failing is a `fail`, not `unclear`.
5. A check may be graded from its recorded evidence without re-reading the whole package, except diagnosis-grounded and test-plan-observable, which always re-read the repro evidence block before grading.
6. Grade the thing itself, not its shape: do not pass or fail a check for headings, length, or polish.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
1. List every check's grade.
2. Apply the rubric's verdict rule: accept only if every required check is `pass`. Any `fail` or `unclear` on a required check gives reject. `unclear` is counted as `fail`.
3. Output `accept` or `reject` only. There is no third verdict.
4. In the output, quote the deciding evidence for each failed or unclear check. If the verdict is accept, quote the evidence for the weakest passing check.
5. In live mode, add any voice-guide rule the draft comment breaks to the summary, quoting the rule. Note any gap where this procedure was silent.
6. End with the JSON block, valid and last.
