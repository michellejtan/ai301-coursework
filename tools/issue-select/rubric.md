# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| repo-active | The dates of the last 5 commits, and the date of the newest release, in Repo facts | Someone made a commit, or the project put out a release, within the last 180 days (counting back from the capture date) | required |
| not-archived | The `archived:` line in Repo facts | The repo is not archived | required |
| bounded-change | The issue's title, body, labels, and comments | The issue asks for one clear thing: one bug fixed, one doc written, or one behavior changed. It's fine if it also lists small extra edits, as long as they all help make that one thing happen. It fails if: the issue is really a list of separate jobs meant for different people, it's just a question asking for help, people are still arguing over how to fix it and no maintainer has decided, or it mixes in unrelated work | required |
| workable-spec | The issue body, and any listed acceptance criteria | A bug report says what goes wrong or how to make it happen. A doc task says which file or section needs the change. A feature request says exactly what it should do. A short bug report from a Member, Owner, or Collaborator that names the problem also counts, even if it's brief | required |
| no-stale-attempts | How old the issue is, its comments, and any linked pull requests | If the issue is older than 365 days, it passes only if it does NOT show people claiming it more than once and then dropping it, and does NOT have 2 or more closed pull requests that already tried to fix it and failed | required |
| ai-policy-compatible | The contribution-policy line in Repo facts | The project says nothing about AI, or it allows AI help (maybe with rules like disclosing it, testing it, or having a person review it). It fails only if the project says AI-written code or docs are not allowed | required |
| unassigned | The assignees list in Repo facts | No person is assigned to the issue | required |
| no-active-pr | Linked pull requests in Repo facts, plus any pull requests mentioned in the comments | No open pull request is already trying to fix this issue | required |
| maintainer-response | The 5-issue sample of maintainer reply times in Repo facts | At least one of those 5 issues got a reply from an Owner, Member, or Collaborator within 90 days of being opened | preferred |
| no-recent-claim | The issue's comments and their dates | Nobody said "I'll work on this" (or similar) in the 14 days before the capture date | preferred |
| good-first-issue-label | The issue's labels | The issue has a label like "good first issue" | preferred |
| visible-adoption | The star count in Repo facts | The repo has 50 or more stars | preferred |

## Verdict rule

Accept only if the issue passes every required check: repo-active,
not-archived, bounded-change, workable-spec, no-stale-attempts,
ai-policy-compatible, unassigned, and no-active-pr. If a required check
fails, or we can't tell (`unclear`), reject the issue — `unclear` counts
as a fail. Preferred checks never change accept/reject; they just help
rank the issues that already passed, using the fit profile in `scope.md`.
