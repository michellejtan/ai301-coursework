# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

michellejtan

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-6032249165

Plan for #73, from my repro above (main at `2f4e82f`).

**Cause.** The repro shows the README (line 24) telling you to add `OPENROUTER_API_KEY`, while `.env.example` has only `LLM_PROVIDER=mock` and `OPENAI_API_KEY` and its provider comment offers only `mock` and `openai`. `core/config.py` lines 20-22 define `openrouter_api_key`, `openrouter_base_url` and `openrouter_model`. So the example file is the one that is out of date.

**Change (one change).** In `.env.example`, add `OPENROUTER_API_KEY=`, add the optional base URL and model as commented lines with the defaults from `core/config.py`, and update the `LLM_PROVIDER` comment. I'll touch README.md line 24 only if it still misleads after that. I won't change `core/config.py`, any application code, or `docs/SETUP.md` (it repeats the same instruction and will already be correct; I'll point it out in the PR).

**Check.** I'll re-run my three repro greps. Before, `.env.example` returned no OPENROUTER line; after, it should return `OPENROUTER_API_KEY` and the provider comment should name openrouter. I'll also run `cp .env.example .env` in a scratch copy and grep the result for `OPENROUTER_API_KEY`.

**Unsure about.** I haven't confirmed that `LLM_PROVIDER=openrouter` is a value the app accepts. The settings class defines it as a free string and I found no code that reads it, so I'll word the comment from what `core/config.py` defines and say so in the PR. If a maintainer wants the wording different, I'll use that.

I'll follow the CONTRIBUTING branch and commit conventions and open a PR once this is built.
---

## Your branch

**Branch**

[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]

docs/73-env-example-openrouter

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

Before (my Unit 2 repro, source revision `2f4e82f`):

```
$ grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" README.md
24:# Configure environment (add your OPENROUTER_API_KEY to .env)

$ grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" .env.example
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here

$ grep -n -i "openrouter\|openai\|LLM_PROVIDER\|API_KEY" core/config.py
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
21:    openrouter_base_url: str = Field(default="https://openrouter.ai/api/v1")
22:    openrouter_model: str = Field(default="google/gemma-3-27b-it:free")
```

After (same commands, on branch `docs/73-env-example-openrouter` with the change):

```
$ grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" README.md
24:# Configure environment (add your OPENROUTER_API_KEY to .env)

$ grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" .env.example
17:# Options: "mock" (default, no API key needed), "openai", "openrouter"
19:LLM_PROVIDER=mock
20:OPENAI_API_KEY=sk-your-key-here
21:OPENROUTER_API_KEY=
22:# Optional OpenRouter settings (defaults from core/config.py)
23:# OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
24:# OPENROUTER_MODEL=google/gemma-3-27b-it:free

$ grep -n -i "openrouter\|openai\|LLM_PROVIDER\|API_KEY" core/config.py
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
21:    openrouter_base_url: str = Field(default="https://openrouter.ai/api/v1")
22:    openrouter_model: str = Field(default="google/gemma-3-27b-it:free")

$ cp .env.example /tmp/test.env
$ grep -n OPENROUTER_API_KEY /tmp/test.env
21:OPENROUTER_API_KEY=
```

`.env.example` now lists `OPENROUTER_API_KEY`, which the README tells the reader to set, and every `openrouter_*` field in `core/config.py` has a matching entry (active or commented). `make lint` was not run: `.venv/bin/ruff` is not installed in my clone and no Python files changed.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1. `--limit 3` smoke test, first draft of the rubric, evidence guide and procedure: 3/3 agreement
2. Full run with `--save-run eval-run.txt`: 19/20 agreement. `pkg-14` disagreed (gold accept, graded reject; failed on `executable-by-stranger` and `honest-about-unknowns`)
3. `--only pkg-14,pkg-10,pkg-17,pkg-01,pkg-16` after loosening those two checks: 5/5 agreement
4. Full run with `--save-run eval-run.txt` (final): 19/20 agreement, bar 18/20 PASS. `pkg-14` now agreed; `pkg-20` (thread-convention) disagreed, graded accept against gold reject. Category line: `clear-accept 7/7  scope-creep 4/4  thread-convention 1/2  unbuildable 3/3  wrong-cause 4/4`

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

`pkg-14` (source: zellij-org/zellij#5174). Gold label: `accept` ("honestly scoped-down: reattach handshake fix with a regression-window repro; defers the untestable Windows variant and says so; arguable on the deferral, ready as scoped"). My rubric's first full run: `reject`, failed on `executable-by-stranger` and `honest-about-unknowns`. After the revision below, it graded `accept` and agreed.

The plan names the reattach path in `zellij-server` and `zellij-client` but not exact functions, and says they will be "pinned in the PR after tracing the query issuance with debug logs, which I have working". My first `executable-by-stranger` wanted named files or functions that exist, so it read that as not executable. The same plan infers a mechanism (responses arrive as input because stdin is wired before they are consumed) from the repro's control runs, and defers the Windows variant it cannot test. My first `honest-about-unknowns` read the inferred mechanism as a guess written as fact. Both readings graded the plan's shape instead of whether a stranger could start and whether it claims more than the repro shows.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

`executable-by-stranger` currently reads: "Someone who has never seen this plan could start work without asking the author anything: the files or functions named are real (in eval mode, a named path is real unless the package contradicts it; the bundle carries no file listing, so do not fail a plausible path for being unverifiable), the approach says what is changed in each, and the order of work is clear. A plan may name a component or code path instead of exact functions when it also gives the concrete first step that pins them down (for example, tracing with debug logs it says it has working); that still lets a stranger start. Fails if the approach is only a goal ("fix the bug", "improve handling"), no file or area is named at all, a named file is invented, or a step depends on information the plan never gives."

It reads that way because of two packages. `calib-01` named one file that an eval bundle cannot verify, so I added that a plausible path the package does not contradict counts. `pkg-14` failed for naming a component instead of exact functions, so I added the sentence that a component plus a concrete first step is enough. I kept the fail conditions for a goal-only approach, no file or area named, and an invented file, because those are what make a plan something a stranger cannot start. I rejected simply dropping the "files are real" requirement, since that would let a plan with no files pass.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

Loosening `executable-by-stranger` and `honest-about-unknowns` fixed `pkg-14` but could let a bad plan through. I re-ran `--only pkg-14,pkg-10,pkg-17,pkg-01,pkg-16`, with `pkg-10` and `pkg-17` (unbuildable) and `pkg-01` and `pkg-16` (wrong-cause) as canaries, and all four stayed reject (5/5). The confirming full run kept every other package as it was.

What the revision gives up: a plan that names only a component and a vague first step could now pass `executable-by-stranger`. The sentence requires a concrete first step, but that is a judgment call the grader makes.

`pkg-20` (thread-convention) flipped from agree to disagree between my first and second full runs, which is why that category ended at 1/2. I did not touch a comms check between them, so it may be run-to-run variation in the grader, but I did not re-run `pkg-20` alone to confirm. I accept that risk because the bar and the category floor both passed. With only two thread-convention packages, a run that missed both would fail the floor, so that is the case my rubric is most exposed to.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
