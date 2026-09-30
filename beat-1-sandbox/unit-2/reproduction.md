# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

michellejtan

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5903358346

Hi! I'd like to take this on as a first contribution.

I see the mismatch: README.md tells you to set OPENROUTER_API_KEY in .env, but .env.example never lists that variable, its LLM_PROVIDER comment only offers mock and openai, even though core/config.py supports both openai and openrouter as providers.

Next I'll go through core/config.py to confirm exactly which env vars each supported provider needs, update .env.example to list all of them with accurate comments, and bring the README wording in line with that. I'll report back here once I've reproduced the confusion and before opening a PR.

**Reproduction comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5905692418

Environment

OS: Ubuntu 24.04.2 LTS
Architecture: x86_64
Relevant versions: none apply — no application code was run for this reproduction (Git 2.48.1 was used only to check the source revision below)
Code state: Path Review repository https://github.com/codepath/pathreview-ai301-fa26-s3, source revision 2f4e82f (working tree clean when inspected)

Steps

1. Open issue #73 ("README and .env.example disagree about which LLM API key to set") and read the reported discrepancy.
2. Searched the README for LLM config instructions:
```bash
grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" README.md
```
3. Ran the same search on `.env.example`:
```bash
grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" .env.example
```
4. Checked which settings the code actually defines:
```bash
grep -n -i "openrouter\|openai\|LLM_PROVIDER\|API_KEY" core/config.py
```
5. Compared the three outputs: what the README tells you to set, what .env.example actually documents, and what the Settings class actually defines.

Evidence

README.md — output of the grep in step 2:
```
24:# Configure environment (add your OPENROUTER_API_KEY to .env)
```

.env.example — output of the grep in step 3:
```
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
```
No `OPENROUTER_API_KEY` line appears anywhere in the file — the same case-insensitive search for "openrouter" that found a match in README.md returns nothing at all from `.env.example`.

core/config.py — output of the grep in step 4:
```
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
21:    openrouter_base_url: str = Field(default="https://openrouter.ai/api/v1")
22:    openrouter_model: str = Field(default="google/gemma-3-27b-it:free")
```
The Settings class defines `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model` fields (`openrouter` is a real, supported provider in the code, just not documented in `.env.example`).

Result

The README tells a new contributor to set OPENROUTER_API_KEY, but .env.example (the file that same contributor is told to copy to .env)  never mentions that variable, and its LLM_PROVIDER comment names only mock and openai as options. core/config.py shows why this matters: the application already defines real configuration fields for openrouter_api_key, openrouter_base_url, and openrouter_model, so openrouter support exists in the code but is invisible in the setup docs and the example file. A contributor following the README and .env.example together has no way to discover the correct variable name (exactly the discrepancy the issue reports).

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `--limit 5` smoke test, on the current 5-check rubric: 5/5 agreement
2. Full run (no `--save-run`): 19/20 agreement — `pkg-10` disagreed, failed on `behavior-matches-issue`
3. `--only pkg-10,pkg-09,pkg-16,pkg-17,pkg-20` after rewriting that check's cannot-reproduce condition into two explicit branches: 4/5 agreement — `pkg-10` now agreed, but `pkg-20` flipped to a disagreement (graded `accept` against gold `reject`)
4. `--only pkg-20` alone, to isolate the flip: 1/1 agreement, `reject` — confirmed the flip was run-to-run grading variance, not a real regression (the edit never touched `comms-respects-conventions`, the check `pkg-20` depends on)
5. Full run with `--save-run eval-run.txt` (committed, final): 20/20 agreement — bar (18/20) PASS

**Package analysis**

`pkg-10` (source: starship/starship#7648). Gold label: `accept` — "honest cannot-reproduce: exact layout and config, prompt artifact shown, names the environment differences (Linux+zsh vs macOS+fish) and the PWD-resolution hypothesis for why fish matters." My rubric's first full run: `reject`, failed on `behavior-matches-issue`.

The report is a genuine, well-evidenced cannot-reproduce: it runs the exact symlink/config layout from the issue, quotes the actual prompt output (which renders normally, unlike the issue's blank prompt), and names precisely what differed from the reporter's setup (shell: zsh vs. fish; OS: Linux vs. macOS) plus a concrete hypothesis for why the shell matters (fish resolves `PWD` logically, which the `contract_repo_path` failure path needs). My check's pass condition at the time stated the general reproduction rule ("a real artifact... showing that same trigger's symptom") and only added the cannot-reproduce exception as a trailing sentence after it. A strict reading of that ordering treats the general rule as the binding requirement and the exception as a footnote, so the check failed a report whose artifact correctly shows *no* bug, because it doesn't show the *same symptom* — exactly backwards for an honest cannot-reproduce.

**Check rationale**

`behavior-matches-issue` currently reads: "Pass if either branch holds. (A) Claimed reproduction: the same relevant input and scenario the issue describes is used — small changes are okay only if the report explains why they still test the same behavior — and a real artifact from an actual attempt is quoted (not an assertion alone) showing that same trigger's symptom. (B) Claimed cannot-reproduce: a genuine attempt at the same trigger is shown (the same input/scenario, or an explained substitute) with a quoted artifact from that attempt showing no bug, and the report names what differed from the issue's environment or scenario. Branch B is a full pass on its own — it is not a partial credit note under branch A, and an honest, well-explained cannot-reproduce should never be graded against branch A's 'shows the same symptom' language. Fails if: no real artifact is quoted at all, a claimed reproduction shows a different symptom without explaining why it is still the same issue, or a claimed cannot-reproduce shows no real attempt."

I rewrote it this way after `pkg-10` (above) failed under the previous, single-paragraph version. The old wording stated the "artifact must show the same symptom" requirement first and tacked the cannot-reproduce exception on as a trailing sentence, which reads as a footnote to the main rule rather than a fully separate, equally valid way to pass. Splitting it into explicit, labeled branches — with a sentence stating outright that branch B is "not a partial credit note under branch A" — removed that ordering ambiguity. I chose this over just deleting the "shows the same symptom" language entirely, because that language is still doing real work: it's what correctly rejects `pkg-02`, `pkg-08`, `pkg-16`, and `pkg-17`, all wrong-target packages where a different symptom is shown and *not* honestly explained as a deliberate cannot-reproduce attempt.

**Trade-offs**

After rewriting `behavior-matches-issue`, I re-ran `pkg-20` (the one-package `disclosure` category) as a canary, even though the edit never touched `comms-respects-conventions`, because the same `--only` batch that fixed `pkg-10` had also shown `pkg-20` flip to `accept`. Isolating it alone (run 4 above) reproduced `reject` again, and the saved per-check JSON showed `comms-respects-conventions` still correctly failing `pkg-20` on the missing AI-usage disclosure, with every other check passing on its genuinely excellent repro. Nothing changed there, and that JSON output is how I know: the earlier `accept` was pure LLM-judge variance on an unrelated check, not a hole opened by my edit.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
