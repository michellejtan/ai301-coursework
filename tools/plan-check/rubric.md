# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The plan's stated cause, read against the repro evidence block (the quoted commands, output, or error text) and the issue's symptom. | The stated cause explains the behavior the repro evidence actually shows, and ties to a specific observation in it (it may quote the line or point to a numbered repro step; a terse cause that is directly consistent with the repro's steps passes) rather than only asserting a cause. The plan targets the cause the evidence points at, not a downstream symptom; a fix that would only hide or catch the symptom while the evidence points upstream fails. Fails if the cause contradicts the repro evidence, ignores it, or rests on behavior the repro never showed. | required |
| scope-bounded | The plan's in-scope statement, its not-in-scope line, and the files or areas it names, read against the issue's ask. | The plan describes one bounded change that answers the issue: it says what will change and what will not, and every file or area named is needed for that change. Fails if it bundles unrelated cleanup, refactors, or extra features (a drive-by rewrite), or names no boundary at all so the size of the change cannot be judged. | required |
| executable-by-stranger | The plan's files-to-touch list, approach, and order of work, read against the repo-facts block. | Someone who has never seen this plan could start work without asking the author anything: the files or functions named are real (in eval mode, a named path is real unless the package contradicts it; the bundle carries no file listing, so do not fail a plausible path for being unverifiable), the approach says what is changed in each, and the order of work is clear. A plan may name a component or code path instead of exact functions when it also gives the concrete first step that pins them down (for example, tracing with debug logs it says it has working); that still lets a stranger start. Fails if the approach is only a goal ("fix the bug", "improve handling"), no file or area is named at all, a named file is invented, or a step depends on information the plan never gives. | required |
| test-plan-observable | The plan's test plan, read against the repro evidence's steps and artifacts. | The test plan re-runs the repro steps (or a check run through the real code) and names an expected result someone could see and compare: the specific output, value, or behavior that differs from the repro's quoted "before." Fails if success is only "it works" or "tests pass", if it names no expected result, or if the check could pass whether or not the bug were fixed. | required |
| honest-about-unknowns | Wherever the plan states its risks and unknowns (if it does), read against how confidently its diagnosis and approach are stated and what the repro evidence actually demonstrates. | Real uncertainty (an untested guess about the cause, an unverified assumption about the code, a risk to other behavior) is stated as uncertain, and nothing is presented as certain that the repro evidence does not demonstrate. A mechanism the plan infers from the repro (including its control runs) and that explains every observation there is not overclaiming; neither is a deliberate, reasoned deferral of something the author cannot test, when the plan says so. Fails if guesses are written as fact, the diagnosis asserts something the repro evidence contradicts or cannot support at all, or claims more than the repro evidence shows, or the plan promises an outcome (a guaranteed fix, a date) it cannot know. A short plan that states no unknowns passes when its cause is directly supported by the repro and it claims nothing beyond that. Judge what the plan claims, not whether it has a section for unknowns or a Deviations heading. | required |
| comms-thread-aware | The plan comment's own text, read against the issue thread's maintainer signals (thread highlights, or the live thread) and the repo-facts block's stated templates, contribution asks, and AI-use policy. | Pass if: (a) the comment responds to this issue and its setting (what the thread says, or when the thread is empty, the repo's stated contribution norms) rather than reading as boilerplate that fits any issue; if the thread holds explicit maintainer direction, ignoring it fails; (b) it meets any condition the repo states (a required template, a contribution ask, disclosure of AI assistance when the policy requires it; silence in the policy requires nothing); (c) it states the plan itself (cause, scope, approach) and not "same approach as above"; (d) it promises no outcome not yet known (a guaranteed fix, a merge, a specific date); saying it will send a PR is an intention, not an outcome, and passes. | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept only if every required check grades pass. If any required check grades fail or unclear, the verdict is reject. `unclear` counts as `fail`: a plan whose evidence cannot be verified from the package is not ready to build from. Preferred checks never change the verdict (this rubric has none).
