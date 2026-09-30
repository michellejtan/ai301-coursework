# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
issue-select: grade these candidate first issues: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62

● Skill(issue-select)
Successfully loaded skill

  Read 3 files, ran 14 shell commands

Summary

Repo facts (apply to all three): last commit 2026-09-16 (6 days ago) → repo-active pass; not-archived pass (archived: false); 0 releases but recent commits are enough; stars = 4 (< 50) → visible-adoption fails (preferred only); docs/CONTRIBUTING.md says nothing about AI, and explicitly documents the seeded-bug/xfail workflow → ai-policy-compatible pass (silence). Course house rule: student claim comments never block claiming here.

┌─────────────────────────┬─────────────────────┬────────────────────────────────────────┬───────────────────┬────────────┬──────────────┬─────────────────────────┬───────────────────────────┬────────────────────────────┐
│          Issue          │   bounded-change    │             workable-spec              │ no-stale-attempts │ unassigned │ no-active-pr │ good-first-issue-label  │  no-recent-claim (pref)   │ maintainer-response (pref) │
│                         │                     │                                        │                   │            │              │         (pref)          │                           │                            │
├─────────────────────────┼─────────────────────┼────────────────────────────────────────┼───────────────────┼────────────┼──────────────┼─────────────────────────┼───────────────────────────┼────────────────────────────┤
│ #73                     │                     │                                        │                   │ pass —     │              │                         │                           │ fail (no maintainer reply  │
│ (README/.env.example    │ pass — one doc fix  │ pass — names both files, exact fix     │ pass — 6 days old │ none       │ pass — none  │ pass                    │ pass (no comments)        │ in 5-issue sample)         │
│ mismatch)               │                     │                                        │                   │            │              │                         │                           │                            │
├─────────────────────────┼─────────────────────┼────────────────────────────────────────┼───────────────────┼────────────┼──────────────┼─────────────────────────┼───────────────────────────┼────────────────────────────┤
│ #69 (output_parser      │ pass — one bug +    │ pass — exact crash, exact files, test  │ pass — 12 days    │ pass —     │              │                         │ overridden by house rule  │                            │
│ array crash)            │ its xfail marker    │ to un-xfail                            │ old               │ none       │ pass — none  │ pass                    │ (2 student claims,        │ fail                       │
│                         │                     │                                        │                   │            │              │                         │ ignored)                  │                            │
├─────────────────────────┼─────────────────────┼────────────────────────────────────────┼───────────────────┼────────────┼──────────────┼─────────────────────────┼───────────────────────────┼────────────────────────────┤
│ #62 (health check       │ pass — one bug,     │ pass — exact cause, repro steps,       │ pass — 12 days    │ pass —     │              │                         │ overridden by house rule  │                            │
│ redis_host)             │ repro steps given   │ confirmed as issue #62 in              │ old               │ none       │ pass — none  │ pass                    │ (1 student claim,         │ fail                       │
│                         │                     │ CONTRIBUTING.md's seeded-bug list      │                   │            │              │                         │ ignored)                  │                            │
└─────────────────────────┴─────────────────────┴────────────────────────────────────────┴───────────────────┴────────────┴──────────────┴─────────────────────────┴───────────────────────────┴────────────────────────────┘

All three pass every required check → accept all three.

Ranking by fit (JS/Node strongest, welcomes a well-scoped Python issue, wants to avoid heavy ramp-up in unfamiliar stacks — all three are Python, none touch the frontend, so I ranked by how bounded/low-ramp-up each is):

1. #73 — smallest, purely a two-file text/config reconciliation, no logic to trace, 1–2 hr estimate. Best low-risk entry point.
2. #62 — small, single-attribute Python fix with a clear repro and an explicit maintainer-documented pointer (api/routes/health.py, attr-defined suppression to remove).
3. #69 — still bounded, but requires understanding the RAG output-parser's fallback logic and an xfail-marked test, more moving parts than the other two.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
    "checks": [
      {"name": "repo-active", "grade": "pass", "evidence": "last commit 2026-09-16, 6 days before capture"},
      {"name": "not-archived", "grade": "pass", "evidence": "archived: false"},
      {"name": "bounded-change", "grade": "pass", "evidence": "body: 'Make the two files agree' naming README.md and .env.example only"},
      {"name": "workable-spec", "grade": "pass", "evidence": "names exact conflicting values (OPENROUTER_API_KEY vs mock/openai) and the two files to fix"},
      {"name": "no-stale-attempts", "grade": "pass", "evidence": "opened 2026-09-16, well under 365 days"},
      {"name": "ai-policy-compatible", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI restriction"},
      {"name": "unassigned", "grade": "pass", "evidence": "assignees: []"},
      {"name": "no-active-pr", "grade": "pass", "evidence": "no cross-referenced PRs, 0 comments"},
      {"name": "maintainer-response", "grade": "fail", "evidence": "5-issue sample (#69-73) shows only NONE-association student replies, no maintainer reply"},
      {"name": "no-recent-claim", "grade": "pass", "evidence": "0 comments on the issue"},
      {"name": "good-first-issue-label", "grade": "pass", "evidence": "labels include 'good first issue'"},
      {"name": "visible-adoption", "grade": "fail", "evidence": "stargazers_count: 4"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62",
    "checks": [
      {"name": "repo-active", "grade": "pass", "evidence": "last commit 2026-09-16, 6 days before capture"},
      {"name": "not-archived", "grade": "pass", "evidence": "archived: false"},
      {"name": "bounded-change", "grade": "pass", "evidence": "single fix: use settings.redis_url instead of nonexistent redis_host/redis_port"},
      {"name": "workable-spec", "grade": "pass", "evidence": "body gives exact file, field names, and reproduction steps (GET /health, 503, AttributeError)"},
      {"name": "no-stale-attempts", "grade": "pass", "evidence": "opened 2026-09-10, 12 days before capture"},
      {"name": "ai-policy-compatible", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI restriction"},
      {"name": "unassigned", "grade": "pass", "evidence": "assignees: []"},
      {"name": "no-active-pr", "grade": "pass", "evidence": "no cross-referenced PRs found; comment thread has no PR mention"},
      {"name": "maintainer-response", "grade": "fail", "evidence": "5-issue sample shows no maintainer (Owner/Member/Collaborator) reply"},
      {"name": "no-recent-claim", "grade": "fail (overridden by house rule)", "evidence": "student comment 2026-09-21 'I would like to work on this issue' — house rule: student claims don't block"},
      {"name": "good-first-issue-label", "grade": "pass", "evidence": "labels include 'good first issue'"},
      {"name": "visible-adoption", "grade": "fail", "evidence": "stargazers_count: 4"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
    "checks": [
      {"name": "repo-active", "grade": "pass", "evidence": "last commit 2026-09-16, 6 days before capture"},
      {"name": "not-archived", "grade": "pass", "evidence": "archived: false"},
      {"name": "bounded-change", "grade": "pass", "evidence": "single bug fix plus removing its own xfail marker, same task"},
      {"name": "workable-spec", "grade": "pass", "evidence": "body names exact crash (.items() on a list), the file, and the test/marker to remove"},
      {"name": "no-stale-attempts", "grade": "pass", "evidence": "opened 2026-09-10, 12 days before capture"},
      {"name": "ai-policy-compatible", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI restriction"},
      {"name": "unassigned", "grade": "pass", "evidence": "assignees: []"},
      {"name": "no-active-pr", "grade": "pass", "evidence": "no cross-referenced PRs found; comment thread has no PR mention"},
      {"name": "maintainer-response", "grade": "fail", "evidence": "5-issue sample shows no maintainer reply"},
      {"name": "no-recent-claim", "grade": "fail (overridden by house rule)", "evidence": "two student claim comments 2026-09-20/21 — house rule: student claims don't block"},
      {"name": "good-first-issue-label", "grade": "pass", "evidence": "labels include 'good first issue'"},
      {"name": "visible-adoption", "grade": "fail", "evidence": "stargazers_count: 4"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1. `--limit 5` smoke test, initial rubric draft: 3/5 agreement
2. `--limit 5` smoke test, rubric rewritten (merged checks + reworded): 5/5 agreement
3. Full run (no `--limit`, no `--save-run`): 19/20 agreement
4. Full run with `--save-run eval-run.txt`: 18/20 agreement — bar 18/20 PASS
5. `--limit 5` smoke test after fixing an enum contract violation (a live-mode
   run had emitted `"grade": "fail (overridden by house rule)"`, outside the
   declared `pass|fail|unclear` domain; reworded `no-recent-claim` and added
   an explicit grade-domain rule to the verdict section): 5/5 agreement
6. Full run with `--save-run eval-run.txt` (committed, final): 18/20
   agreement — bar 18/20 PASS

Runs 3 and 4 used the exact same rubric file, with no edit between them, yet
agreement moved from 19/20 to 18/20: issue-01 flipped to agree, while issue-19
and issue-20 flipped to disagree. That's pure run-to-run grading variance from
the LLM judge, not a rubric change (worth naming so it's clear how much of
this score reflects the rubric itself versus noise between identical runs).
Runs 4 and 6 bracket a real rubric edit (the enum-domain fix) and landed on
the identical 18/20 with the identical two misses, which is itself useful
confirmation that the fix was cosmetic for eval-mode grading, exactly as
expected, since the Path Review house rule it touches never applies outside
live mode.

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

`issue-19` (source: zxcalc/zxlive#517). Gold label: `accept` ("maintainer-diagnosed
performance bug with named causes, unclaimed"). My rubric's verdict: `reject`, failed on
`bounded-change`. The issue body names two causes of a UI freeze (slow matchers, blocking
UI thread) plus three follow-up suggestions (multi-processing, selective matching,
threading the rewrite step). My `bounded-change` check reads this as multiple separate
work items rather than one bug with several contributing causes and possible fix angles,
so it rejected an issue that's really one coherent "fix the freeze" task.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

`bounded-change` currently reads: "The issue asks for one clear thing: one bug fixed, one
doc written, or one behavior changed. It's fine if it also lists small extra edits, as
long as they all help make that one thing happen. It fails if: the issue is really a list
of separate jobs meant for different people, it's just a question asking for help, people
are still arguing over how to fix it and no maintainer has decided, or it mixes in
unrelated work." 
This check is meant to identify tracking or umbrella issues while still allowing one issue to explain its fix in several parts. I wrote it this way after my rubric wrongly rejected #73 (a docs task listing several related file edits) for looking like a multi-part job when it was really one page's rollout. So the check should not fail an issue just because it is long or has several bullet points — it should fail only when it actually contains separate tasks meant for different people.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This method may miss some issues, such as issue-19. For example, one bug may have several causes or several possible ways to fix it. The grading system (rubric) may mistakenly see these as separate tasks, even though the maintainer considers them part of one fix.

Changing the rule to clearly include “several causes or possible solutions for the same bug” could fix this problem. However, it could also create a new problem by allowing a large issue with several separate tasks to be counted as one task.

I decided to leave the rule as it is instead of changing it just to fix one issue. The rubric already meets the required score and the minimum requirements for each category.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

1. I chose #73 because it is a small and simple task that only involves two files. It does not require me to work with complicated code. Since I am still learning how the project works, I think this is a good task for my first contribution. It will also give me time to learn the testing and pull request process.

2. The verdict correctly showed that all three tasks (#73, #62, and #69) were available to work on and followed the project rules. However, it did not consider how much time I had or how comfortable I was with each task. I chose #73 because I wanted to start with a task that had less risk. Although #62 and #69 would give me more practice with Python, I felt that #73 was a better choice for my first contribution.

3. I expect #73 to be fairly easy because I will not need to change complicated code. The main task is to make sure that two files are correct and match each other. The more difficult part may be setting up my computer so the project works properly, including the development environment and the .env file.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
