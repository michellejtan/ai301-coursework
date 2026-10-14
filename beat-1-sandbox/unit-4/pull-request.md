# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

<PASTE YOUR PR PAGE LINK HERE: https://github.com/codepath/pathreview-ai301-fa26-s3/pull/<number>>

**Branch**

`docs/73-env-example-openrouter`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. First full run: 13/20. Every one of the 7 `clear-accept` packages was wrongly rejected (`category: clear-accept 0/7`, floor unmet).
2. Partial `--only` re-grade of the 7 wrong rows plus canaries `pkg-01`, `pkg-20`, `pkg-04`, `pkg-07`: 11/11 (partial, so no bar verdict).
3. Confirming full run: 19/20 (`agreement: 19/20 scored items  (bar: 18/20: PASS)`). This is the run in `eval-run.txt`.

**Package analysis**

**pkg-11** (`clear-accept`, the ripgrep trailing-space parser fix). Gold label: `accept`. My rubric: `accept`, every check passed.

The description says tests were added "for the escaped, unescaped, and double-backslash cases", but the diff adds one test function that covers the escaped case and the double-backslash case. On my first full run `description-matches-diff` failed this package for that wording. I revised the check to say "A loosely worded claim the diff substantially supports (for example a test described as several cases when one test covers them) passes", because the change the description claims, stopping the trim at an escaped space, is exactly what the diff does. The test evidence also quotes the before error (`dangling '\'`), the after behavior, and `cargo test -p ignore` passes (214 tests), so `tests-observable` passes. The description also carries the AI-use disclosure the repo's policy asks for ("this change was AI-assisted with me reviewing and understanding every line"), so `standards-met` passes.

**Check rationale**

My `tests-observable` check, exactly as it reads in `tools/pr-precheck/rubric.md`:

| tests-observable | The test evidence (the repro re-run before and after, and the output of the repo's own checks named in the PR template), read against the plan's test plan. | The evidence shows an observable before/after difference from the plan's repro (specific output, value, or behavior that differs and matches the plan's expected result), and the repo's own checks (the commands the repo's template or the package names) were run with a stated result. A check that fails or stops (for example "no tests ran") passes when the result is reported honestly with the reason. Fails if the evidence is only "it works" or "tests pass", could pass whether or not the bug were fixed, omits the before or the after, shows a different scenario than the plan's repro, states no result for the repo's checks, or reports a result the pasted output contradicts. The before and after must quote concrete observed output (the error text, value, or rows the run produced), whether as a command transcript or as annotated lines in one; a vague note such as "works now" or "colors work" with no quoted output fails. Once that decisive before/after is shown, a control run the plan names, and the result of the repo's test command, count when the package states a concrete result for them (an exit code, a quoted line, or "N tests passed"), even without a full transcript; they fail if the result is missing, vague, or contradicted by the pasted output. Claims in the description's Testing section must be backed by the pasted output. | required |

Why it reads this way: my first version required a pasted transcript for every control run and every repo check, and treated a typed "tests pass" as a claim that fails. That rejected all 7 `clear-accept` packages, because they quote concrete before/after output for the repro and then give a one-line result for the suite (for example `cargo test -p nu-protocol` passes (312 tests)). I kept the part that matters, the before and after must quote concrete observed output, and loosened the rest so a control run or the test command counts when it states a concrete result (an exit code, a quoted line, or a test count). A vague note like "colors work now" (pkg-04) still fails.

**Trade-offs**

Loosening `tests-observable` cost me pkg-13. It agreed (accept) in my partial `--only` re-grade, but in the confirming full run it was rejected on `tests-observable` (`clear-accept 6/7`). It is a `clear-accept` package whose plan names a no-ampersand control run, so a check that now accepts a stated control result without a full transcript sits close to the line on it, and I accept that it will sometimes reject it. I did not change the rubric again after the 19/20 run, because the fingerprints in `eval-run.txt` have to match the files I uploaded, and the run already clears the 18/20 bar and the category floor. The canaries I re-ran with `--only` (pkg-01 and pkg-20 for `standards-wall`, pkg-04 and pkg-07 for `not-tested`) all kept agreeing after the loosening.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
