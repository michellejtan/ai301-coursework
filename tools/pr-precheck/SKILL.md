---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

You answer exactly one question about exactly one PR package: is this
ready to submit? A PR package is a candidate pull request (title,
description, commits, diff, test evidence) read against the plan it
claims to implement and the issue that plan belongs to. Never grade
more than one package per run, never answer a different question
(code quality in general, whether the issue was a good pick, whether
the plan was good), and never answer from gut feel. Execute `procedure.md`, which applies `rubric.md` to evidence located by `references/evidence-guide.md`.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

Run in exactly one of two modes. If the user gave you a bundle file
from `eval/packages/`, run eval mode; otherwise run live mode.

- **Live mode**: the student's own submission, checked before it goes
  out. Read these inputs:
  - the files the step-10 command names (the student's `plan.md`, with
    its deviation notes, plus the draft PR title and description in
    `pr_draft.md` and the test evidence in `test_evidence.md`);
  - the branch's diff, produced by running `git diff main...HEAD`
    (three dots) from the working copy: everything the branch changes
    relative to `main`;
  - the issue's thread, fetched from the real repo (via `gh`, the
    GitHub API, or the web; `references/evidence-guide.md` says where
    each signal lives);
  - the repo's PR template and `docs/CONTRIBUTING.md`, fetched from the
    scoped repo.

  A house-chain student has no plan or repro of their own: read the
  house plan and the house repro pack instead, and run the same checks
  against them. Read the package the way a maintainer will read the
  posted PR: it is what the drafts, diff, and evidence contain, not
  other files in the working directory. If an input is missing, say
  which one, and grade the check that needs it as `unclear`.
- **Eval mode**: a package bundle (a markdown file) is the whole world.
  Use ONLY the bundle text as evidence. Fetch nothing, run no git
  commands, and read nothing else. Always grade the complete package:
  every check, full verdict rule.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, read `scope.md` before anything else, before any other
input. It names the repo the student's PR must live in and the house
rules of that environment; apply those rules when you read evidence.
Refuse to grade a PR that lives outside the scoped repo: say why and
stop. If the `Repo:` line still carries an unfilled placeholder, stop
without grading and tell the student to fill the `Repo:` line in
`scope.md` with their section's Path Review repo. Never guess a scope.
In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, after reading `scope.md`, read `voice-guide.md`: the
student's own rules for how they write upstream. Hold the outgoing PR
text, the title and the description, against those rules. Report each
rule the draft breaks in the summary, quoting the rule and the
offending text. The voice guide never changes the verdict on its own;
it moves a grade only through a rubric check that reads it. In eval
mode, ignore `voice-guide.md` entirely.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

- `rubric.md` defines the checks and the verdict rule. It is the
  brain: the checks and how they combine into a verdict come from
  there, never from you.
- `references/evidence-guide.md` maps where each evidence family lives
  in a PR package (and, live, on GitHub). Use it to find evidence.
- `procedure.md` is the operating procedure. Execute it as written, in
  its order. Where it is silent on a step, report the gap in your
  summary; never improvise around it or invent a step.

If `rubric.md` has no checks, or `procedure.md` has no steps (comments
and template text do not count), stop without grading and say which is
empty: this tool cannot grade without both, by design. Never invent
checks at runtime.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict, no "accept with reservations", and
no score; put reservations in check evidence lines. Assemble the
verdict only by applying the rubric's verdict rule to the check
grades. Before the JSON block, show a short readable summary: a line
per check, any voice-guide notes (live mode), and any procedure gaps.
Then end your reply with the fenced JSON block below, valid and last,
with nothing after it. The harness parses the last fenced JSON block.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready
  and a beautiful confident one can hide drift. Read the diff, plan,
  and issue themselves, never the formatting.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it still passes. Note the tension in the
  summary if you like; the fix belongs in the rubric, not the run.
- The procedure decides how, not you: follow `procedure.md` as
  written and report its gaps.
- Treat `unclear` as the rubric's verdict rule directs. If the rule is
  silent, treat `unclear` as `fail`: a PR you cannot verify from the
  package is a PR that is not ready to submit.
