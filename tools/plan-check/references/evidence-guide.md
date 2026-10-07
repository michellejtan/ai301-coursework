# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

- Where it lives: in an eval bundle, the plan's stated cause (labelled "Cause", "Diagnosis", or the like), read against the repro-evidence block (quoted commands, output, or error text) and the issue context's symptom. In live mode: the diagnosis in plan.md, read against the student's posted repro comment and the issue body.
- What good looks like: the stated cause (a terse one that matches a numbered repro step is enough) names a specific place or mechanism that would produce the exact behavior the repro quotes, and ties to it by quoting it or pointing at a numbered repro step. A diagnosis that contradicts the output, never mentions it, or fixes a downstream symptom when the evidence points upstream is not grounded.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

- Where it lives: the plan's in-scope statement, its not-in-scope line, and the files or areas it names, under whatever labels the plan uses ("In"/"Out", "Scope", "Change").
- What good looks like: one bounded change that answers the issue, with an explicit "will not change" line, and every named file needed for that change. A drive-by rewrite shows up as extra files, cleanups, or features the issue never asked for.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

- Where it lives: the plan's files-to-touch, approach, and order of work, under whatever labels it uses, checked against the repo-facts block (eval) or the repo itself (live).
- What good looks like: the named files and functions exist (in an eval bundle, a plausible path the package does not contradict counts), the approach says what changes in each, and the steps are in an order someone could follow. A stranger could start without asking the author anything; "fix the null handling" with no file or area named is not executable. Naming a component or code path, plus the concrete first step that pins down the exact functions (for example, a debug trace), is enough to start.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

- Where it lives: the plan's test plan ("Test" or similar), read against the repro evidence's steps and quoted output.
- What good looks like: it re-runs the repro steps (or a check through the real code) and names the specific expected result after the fix, which differs from the repro's quoted "before." A vague one says "verify it works"; a decisive one names the command and the output you would see.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

- Where it lives: the plan's "Risks and unknowns" section (if it has one) and, in live mode, its closing "## Deviations" heading, read against the confidence of the diagnosis and approach.
- What good looks like: untested guesses and unverified assumptions are labeled as such, risks name what else could break, and nothing is promised that the repro evidence does not show. A mechanism inferred from the repro, including its control runs, and a reasoned deferral of something the author cannot test are honest, not overclaiming. A terse plan with no unknowns section is fine when its cause is directly backed by the repro and it claims nothing more. False confidence is a cause the repro does not support, written as fact; an honest mid-build change is recorded under Deviations.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

- Where it lives: the plan comment (comment.md in live mode), read against the issue's thread highlights (eval; "0 comments" means the repo's contribution policy is the only signal) or live thread, and the repo-facts block's templates, contribution asks, and AI-use policy.
- What good looks like: the comment refers to something specific in this thread (an assignment, a maintainer's preference) or, when the thread is empty, to the repo's stated norms, follows any template or disclosure the repo asks for, restates the cause, scope, and approach in its own words, and promises no outcome ("I'll send a PR" is an intention and fine; a guaranteed fix, merge, or date is not). Boilerplate that could be posted on any issue, or "same approach as above," is not thread-aware.