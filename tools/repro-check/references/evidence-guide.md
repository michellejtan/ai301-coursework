# Evidence guide: where proof lives in a reproduction package

Organized by family to match `rubric.md`'s five checks, one per family. Each
heading below names the check it serves and, where relevant, the two
originally-separate checks that were merged into it.

## Environment
_Serves: `environment-recorded` (merged from `environment-target-match` + `environment-recorded`)_

- Where it lives: in an eval bundle, the repro report's own "Environment" line or section (OS, tool version, dependency versions), read against the issue's "Version:" / "Operating system:" line and the repo-facts block's latest-release line. In live mode: the same environment line in the student's draft repro report, read against the issue body and the repo's current release.
- What good looks like: an explicit version/OS statement that either matches the issue's stated target, or — when it doesn't (a newer release, a different OS, an install method the issue didn't use) — says so in the same paragraph, rather than reporting the result as if it confirms the bug on the reporter's exact setup. Silence about a version gap is the failure mode, not the gap itself.

## Steps
_Serves: `steps-followable` (merged from `steps-followable` + `steps-complete`)_

- Where it lives: the repro report's numbered steps or command block. In an eval bundle these are literal text to read as-is; in live mode, check whether a step names a resource (a private repo, an internal config file, an unshared branch) that a stranger reading the posted comment could not obtain.
- What makes steps followable: each step is a command, config snippet, or input a reader could paste and run, in order, reaching the same trigger point the issue names (the same flag, the same input shape, the same sequence) — not a step that stops one action short of the trigger, and not a step whose prerequisite ("set up the project," "configure the monorepo") is never spelled out.

## Behavior shown
_Serves: `behavior-matches-issue` (merged from `behavior-matches-issue` + `issue-match` + `result-match`)_

- Where it lives: any fenced code block, command output, or log excerpt inside the repro report — read side by side with the issue's own quoted output or panic trace, and with the issue's stated input/scenario for the input side specifically. A report that only narrates ("this confirms the bug") without a quoted block has nothing here to check.
- What it means to match: two separate ways to pass, not one rule with an exception bolted on.
  - **Claimed reproduction**: the quoted excerpt shows the same triggering input and the same resulting symptom as the issue (same error class, same crash vs. graceful exit, same wrong value) — not an adjacent symptom (a different error message, a validation failure instead of a panic, the tool merely starting up). A small change to the input is fine only when the report says why it still tests the same behavior.
  - **Claimed cannot-reproduce**: a real attempt at the same trigger is shown (a genuine command/config, not skipped), the quoted artifact genuinely shows no bug, and the report names what differed from the issue (environment, shell, OS, config) — this is a complete pass on its own. Do not grade a well-explained cannot-reproduce against the "shows the same symptom" language above; that language is for claimed reproductions only. The giveaway of a good cannot-reproduce is a concrete, falsifiable guess at *why* the difference might matter (e.g. "a fish shell resolving PWD logically looks necessary to hit this"), not just "didn't happen for me."

## Honesty
_Serves: `evidence-based` (merged from `evidence-based` + `honest-outcome`)_

- Where it lives: the report's own concluding language ("Analysis," "Expected/Actual," or a closing sentence) compared against the artifact quoted just above it in the same report.
- What separates honest from overclaimed: an evidenced cannot-reproduce ("ran the same steps, saw X instead of Y, and it's likely explained by Z difference") is honest and should pass. A claim of certainty, a diagnosed root cause, or a word like "verified," "guaranteed," or "confirmed" that isn't backed by the artifact directly above it is overclaiming — as is stretching a result tested on one release/config to "the bug" in general, when the maintainers or the issue scope a different one. A report that only asserts "issue confirmed" with no quoted command/input/output anywhere fails here even if its prose sounds confident.

## Comms
_Serves: `comms-respects-conventions`_

- Where it lives: the repo-facts block's "contribution policy" / AI-policy line (an eval bundle) or the repo's `CONTRIBUTING.md`/`AI_POLICY.md`/issue templates (live mode), read against the actual text of the claim comment and repro comment.
- What good looks like: if the policy requires disclosing AI assistance, at least one comment names the tool and the extent of help — silence is a fail there, but silence is a pass wherever the policy itself says nothing or is merely permissive. Separately, a good claim comment names something specific about this issue (a function, a line, a symptom) and a concrete next step, not "I'd like to work on this" alone; and neither comment promises a fix, a timeline, or a guaranteed outcome before the work is done — the promise is only the investigation and the report.
