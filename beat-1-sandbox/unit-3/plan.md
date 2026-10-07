# Plan for #73: README and .env.example disagree about which LLM API key to set

## Diagnosis

The README tells a new contributor to add `OPENROUTER_API_KEY` to `.env` right after `cp .env.example .env`, but `.env.example` never lists that variable, so the file they were told to copy cannot lead them to it. My Unit 2 repro (source revision `2f4e82f`) shows each side:

- README.md: `24:# Configure environment (add your OPENROUTER_API_KEY to .env)`
- .env.example: only `18:LLM_PROVIDER=mock` and `19:OPENAI_API_KEY=sk-your-key-here`. The same case-insensitive search for "openrouter" returns nothing from this file, and its comment offers only `mock` and `openai`.
- core/config.py: `openrouter_api_key`, `openrouter_base_url` and `openrouter_model` are defined as real settings (lines 20-22).

So the cause is that the example file is out of date relative to the settings class and the README, not that the README is wrong. This is a documentation fix; the repro ran no application code.

## Scope

In scope: one change to make the two files named in the issue agree.
- `.env.example`: add `OPENROUTER_API_KEY=` with an empty value (matching the empty default in `core/config.py`), add the optional `OPENROUTER_BASE_URL` and `OPENROUTER_MODEL` as commented-out lines using the defaults from `core/config.py`, and update the `LLM_PROVIDER` comment so it no longer lists only `mock` and `openai`.
- `README.md`: only a wording fix on line 24 if the `.env.example` change leaves it misleading (for example, saying a key is needed when the default `mock` provider needs none).

Not in scope: `core/config.py` or any application code, how `LLM_PROVIDER` is read or validated, and `docs/SETUP.md`. SETUP.md line 47 repeats the same `OPENROUTER_API_KEY` instruction; it will already be correct once `.env.example` lists the variable, so I will mention it in the PR instead of changing it.

## Files I'll touch

- `.env.example` (lines ~17-19, the LLM provider block)
- `README.md` (line 24, only if needed)

## Approach

1. Re-read `core/config.py` lines 17-22 and copy the exact field names and defaults, so the example file matches what the settings class defines.
2. Edit the LLM provider block in `.env.example`: keep `LLM_PROVIDER=mock` as the default, keep `OPENAI_API_KEY`, add `OPENROUTER_API_KEY`, and add the two optional OpenRouter lines commented out.
3. Rewrite the provider comment to name the providers the settings class supports. I will word it from what `core/config.py` defines and will not claim more (see unknowns).
4. Re-read README.md line 24 against the new `.env.example` and edit it only if it still misleads.
5. Run the repo's checks that apply to config and docs files, then open the PR using the PR template.

## Test plan

Re-run my Unit 2 repro steps against the changed files, from the repo root:

```bash
grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" README.md
grep -n -i "openrouter\|LLM_PROVIDER\|API_KEY" .env.example
grep -n -i "openrouter\|openai\|LLM_PROVIDER\|API_KEY" core/config.py
```

Before (my posted repro): `.env.example` returned only `18:LLM_PROVIDER=mock` and `19:OPENAI_API_KEY=sk-your-key-here`, with no `OPENROUTER_API_KEY` line anywhere.

Expected after: the `.env.example` search also returns an `OPENROUTER_API_KEY` line, and the `LLM_PROVIDER` comment names openrouter. Every variable name the README tells the reader to set appears in `.env.example`, and every `openrouter_*` field in `core/config.py` has a matching entry (active or commented). Then `cp .env.example .env` in a scratch copy and check that the resulting `.env` contains `OPENROUTER_API_KEY`. Also run `make lint` to confirm nothing else changed.

## Risks and unknowns

- I have not confirmed that `LLM_PROVIDER=openrouter` is a value the application accepts. `core/config.py` defines `llm_provider` as a free string with default `mock`, and I found no code that reads `llm_provider` or the `openrouter_*` fields. I will word the comment to match what the settings class defines, and I will not claim a behavior I have not seen run.
- Leaving `.env.example` with an empty `OPENROUTER_API_KEY=` could be read as required. I plan to say that it is only needed when using OpenRouter, but the right wording is a judgment call for the maintainer.
- Thread note: this issue has many plans from other students, including some that propose the same `.env.example` change. This plan comes from my own repro and does not depend on theirs.

## Deviations

The build followed the posted plan: one change to `.env.example` (added `OPENROUTER_API_KEY=`, the optional `OPENROUTER_BASE_URL` and `OPENROUTER_MODEL` as commented lines with the defaults from `core/config.py`, and an updated `LLM_PROVIDER` comment). README.md, `core/config.py`, application code and `docs/SETUP.md` were not changed, as planned. I left README line 24 alone because it names a variable that `.env.example` now lists.

Two things differ from what I said I would do:

- I listed `"openrouter"` as an option in the `LLM_PROVIDER` comment, even though the plan says I had not confirmed the app accepts that value. I did this because the issue asks the comment to stop offering only `mock` and `openai`. I still have not seen the value run, and I will say so in the PR so a maintainer can change the wording.
- I did not run `make lint`. The project's `.venv` is not installed in my clone (`.venv/bin/ruff: No such file or directory`), and the change touches no Python files. My check was the three repro greps plus copying `.env.example` to a scratch file and grepping it for `OPENROUTER_API_KEY`.

The posted plan comment is still true, except that it promised to word the provider comment only from what `core/config.py` defines; the `"openrouter"` option goes slightly beyond that, and I will say so in the PR rather than posting a follow-up now.