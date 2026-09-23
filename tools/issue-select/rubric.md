# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Not archived | The repo-facts block's `archived:` line (live mode: the "This repository has been archived" banner on the repo front page) | Pass if the repo is not marked archived; fail if it is | required |
| Repo active | The repo-facts block's "last 5 default-branch commits" and "last push to any branch" dates, measured against the bundle's capture date (live mode: measured against today) | Pass if at least one default-branch commit or push to any branch is dated within the last 180 days; fail otherwise | required |
| Bounded scope | The issue body and comment thread | Fail only if any of: (a) the issue explicitly frames itself as a tracking/meta issue, a checklist of separate issues or PRs meant to be divided among contributors, or an umbrella spanning the whole codebase (e.g. "add X to every module", "tracking issue for X"); (b) the thread contains an actual back-and-forth between the reporter and a maintainer debating what the right fix or design even is, spanning multiple rounds over weeks or longer, that never reaches a stated conclusion (not merely many comments — a long claim/unclaim history from zulipbot-style bots is not design debate by itself, but count it alongside the debate as further evidence of real difficulty); (c) a maintainer states in the thread that the fix requires changes to core internals or architecture; or (d) the issue proposes a brand-new, product-level feature (not a bug fix, not a docs task, not a feature already committed to) that was not opened by someone with Owner/Member/Collaborator association and carries no maintainer comment endorsing or scoping it — even a detailed writeup leaves the real question ("should we build this, and how") for a maintainer to decide first. Do NOT fail for: a numbered or bulleted list of possible causes, implementation suggestions, or sub-parts of ONE described bug or feature (e.g. "1. matchers are slow 2. UI waits on the matching thread" as two causes of one freeze, or "remove identity, fuse spiders, remove self loops" as instances of one preview bug); a docs task touching several related files; or a body that is merely short or informal. Otherwise pass | required |
| Not a support request | The issue body | Fail if the issue is purely a usage question ("how do I get X to work?") with no requested code change; pass if it asks for a bug fix, a defined feature, or a docs change | required |
| Unclaimed | The repo-facts block's "this issue: assignees:" and "linked PRs:" lines, plus the Comments section for claim language ("I'll take this", "working on this", "can I work on this?") | Fail if an assignee is set, OR an open (not closed/merged) linked PR exists, OR a claim comment was posted within 90 days of the bundle's capture date without a maintainer or the claimant later saying it was dropped. Pass if none of these hold — including when the only claim on record is older than 90 days and unresolved (stale), or a maintainer has since invited new takers | required |
| AI contribution policy | The repo-facts block's "contribution policy" line (live mode: `CONTRIBUTING.md`, `.github/`, `AI_POLICY.md`/`AI_USAGE_POLICY.md`, or PR/issue templates) | Fail only if the policy states an outright ban on AI-generated code or contributions. Pass if the policy sets conditions (disclosure, human review, personal testing/understanding) or if the repo states no AI policy at all | required |
| Good-first-issue label | The issue's labels, as shown in the bundle or the issue sidebar | Pass if the issue carries a "good first issue" (or equivalent) label | preferred |
| Maintainer-filed | The issue's opener, per the bundle or the issue's author_association | Pass if the issue was opened by someone with Owner, Member, or Collaborator association | preferred |
| Maintainer engagement | The repo-facts block's "maintainer first-response sample" (live mode: badges next to commenters in a few recently updated issues) | Pass if the sample shows at least one reply from someone with Owner, Member, or Collaborator association within 30 days | preferred |

## Verdict rule

Accept only if every `required` check passes. Any single `required` check
that fails rejects the issue, regardless of how the others graded.
`unclear` on a `required` check counts as a fail for that check (the
evidence needed to verify it is genuinely absent, so the issue cannot be
confirmed safe to accept). `preferred` checks never affect the verdict;
they only order the accepted issues by how many preferred checks they
pass, most first, for ranking against the fit profile in `scope.md`.
