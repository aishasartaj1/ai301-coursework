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

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

**Verdict output**

```
Scope check (scope.md): all three candidates are in codepath/pathreview-ai301-fa26-s1,
the scoped repo — in bounds.

Repo facts (live, checked 2026-09-23): not archived; last push 2026-09-16 (7 days ago,
all authored by Aburke225/COLLABORATOR — the course maintainer); no releases (course
repo, not versioned); docs/CONTRIBUTING.md has no AI-use statement at all (silence).

Ranked read-out

1. #73 — README and `.env.example` disagree about which LLM API key to set — fit:
   smallest, lowest-risk task (docs+config text only, maintainer-stated 1-2 hour
   estimate), matches my stated preference for a smaller well-scoped first issue.
2. #61 — Health check DB probe passes a raw SQL string, fails under SQLAlchemy 2.x —
   fit: single clear backend fix with an exact repro and error message.
3. #57 — Tech detector counts vendored/build-output files, skewing language detection —
   fit: bounded agent-tool bug with a runnable repro and named failing tests, but the
   fix touches path-filtering logic rather than a one-line change, slightly larger than
   #73/#61.

All three: unclaimed (no assignees, no comments, no linked PRs), maintainer-filed,
good-first-issue labeled, bounded single-bug scope, not a support request, repo not
archived and active, no AI-contribution ban.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
  "checks": [
    {"name": "Not archived", "grade": "pass", "evidence": "repo isArchived: false"},
    {"name": "Repo active", "grade": "pass", "evidence": "last push 2026-09-16, 7 days before today (2026-09-23)"},
    {"name": "Bounded scope", "grade": "pass", "evidence": "single two-file text mismatch, maintainer states 'Estimated effort: 1-2 hours', no debate or umbrella framing"},
    {"name": "Not a support request", "grade": "pass", "evidence": "requests a doc/config fix, not a usage question"},
    {"name": "Unclaimed", "grade": "pass", "evidence": "assignees: none; 0 comments; no linked PRs"},
    {"name": "AI contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md states no AI policy; silence passes"},
    {"name": "Good-first-issue label", "grade": "pass", "evidence": "labels include 'good first issue'"},
    {"name": "Maintainer-filed", "grade": "pass", "evidence": "opened by Aburke225, author_association COLLABORATOR"},
    {"name": "Maintainer engagement", "grade": "unclear", "evidence": "issue has 0 comments; small sample of other issues showed only student (NONE) replies, no maintainer reply timing available"}
  ],
  "verdict": "accept"
}
```

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Smoke test, `--limit 5`, first rubric draft (required "Maintainer responsive" check,
   looser "Bounded scope" check): `agreement: 3/5 scored items`. Disagreed on two
   clear-accept issues (issue-01, issue-04), both wrongly rejected.
2. Smoke test, `--limit 5`, after dropping "Maintainer responsive" to a preferred
   check and rewriting "Bounded scope" to distinguish a real tracking/umbrella issue
   from a bounded task that merely lists several related parts: `agreement: 5/5 scored
   items`.
3. Full run (not saved), same rubric as run 2: `agreement: 18/20 scored items  (bar:
   18/20: PASS)`. `categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy
   1/1  scope 2/4`.
4. Confirming full run, `--save-run eval-run.txt`, same rubric as run 3 (no rubric
   change between runs 3 and 4): `agreement: 16/20 scored items  (bar: 18/20: below
   the bar)`. Two previously-correct clear-accept issues (issue-04, issue-19) flipped
   to reject on "Bounded scope" — model variance on the same rubric text, not a rubric
   change.
5. Cheap re-check, `--only issue-01,issue-04,issue-19,issue-05,issue-10,issue-15,
   issue-20`, after rewriting "Bounded scope" again with an explicit "Do NOT fail for"
   carve-out for enumerated causes/sub-parts of one bug: `agreement: 7/7 scored
   items`.
6. Confirming full run, `--save-run eval-run.txt`, same rubric as run 5: `agreement:
   19/20 scored items  (bar: 18/20: PASS)`. `categories: claimed 4/4  clear-accept
   8/8  dead-repo 3/3  policy 1/1  scope 3/4`. This is the run committed as
   `eval-run.txt`.

**Issue analysis**

`issue-15` (category: `scope`). My rubric's verdict: `accept`, in both run 4 and the
committed run 6. Gold label: `reject`, note: "years of design debate and two abandoned
PRs behind a friendly label."

Why my rubric read it differently: the bundle's repo-facts line reads `linked PRs:
zulip/zulip#20840 (closed); zulip/zulip#23123 (closed)`. My "Unclaimed" check's pass
condition only fails an issue for "an open (not closed/merged) linked PR" — two closed,
abandoned attempts don't register at all under that wording. Separately, my "Bounded
scope" check fails an issue only when the thread shows "an actual back-and-forth
between the reporter and a maintainer debating what the right fix or design even is,
spanning multiple rounds over weeks or longer, that never reaches a stated conclusion."
The real debate in the thread is a single quiet 2021 exchange where the maintainer
(`timabbott`) asks, "can you provide an example Slack payload or a pointer to the right
part of their documentation?", and the reporter supplies one a few days later — a
clarifying exchange, not a loud, sustained argument. My rubric read that as a reporter
answering a question, not as a maintainer leaving the design genuinely unsettled, so
neither check fired. Both signals (the closed PRs and the quiet early debate) point the
same way — this issue is harder than its "good first issue" label suggests — but I
wrote both checks to catch a loud, current version of that difficulty, not a quiet,
long-dormant one.

**Check rationale**

Quoted as currently written in `rubric.md`:

> Fail only if any of: (a) the issue explicitly frames itself as a tracking/meta issue,
> a checklist of separate issues or PRs meant to be divided among contributors, or an
> umbrella spanning the whole codebase (e.g. "add X to every module", "tracking issue
> for X"); (b) the thread contains an actual back-and-forth between the reporter and a
> maintainer debating what the right fix or design even is, spanning multiple rounds
> over weeks or longer, that never reaches a stated conclusion (not merely many
> comments — a long claim/unclaim history from zulipbot-style bots is not design
> debate by itself, but count it alongside the debate as further evidence of real
> difficulty); (c) a maintainer states in the thread that the fix requires changes to
> core internals or architecture; or (d) the issue proposes a brand-new, product-level
> feature (not a bug fix, not a docs task, not a feature already committed to) that was
> not opened by someone with Owner/Member/Collaborator association and carries no
> maintainer comment endorsing or scoping it — even a detailed writeup leaves the real
> question ("should we build this, and how") for a maintainer to decide first. Do NOT
> fail for: a numbered or bulleted list of possible causes, implementation
> suggestions, or sub-parts of ONE described bug or feature (e.g. "1. matchers are
> slow 2. UI waits on the matching thread" as two causes of one freeze, or "remove
> identity, fuse spiders, remove self loops" as instances of one preview bug); a docs
> task touching several related files; or a body that is merely short or informal.
> Otherwise pass

This is the "Bounded scope" check. I wrote it in this shape after run 1's eval failed
two clear-accept issues (issue-01, a docs task touching five related files; issue-04, a
bug listing "remove identity, fuse spiders, remove self loops" as one preview feature)
on an earlier, shorter version of this check that simply failed any issue whose body
"describes a checklist/list of multiple ... sub-items." Sonnet was reading any
list-shaped body as an unbounded umbrella unless told explicitly not to, so I added the
named counter-examples and the explicit "Do NOT fail for" carve-out, and tightened the
design-debate clause to require an actual, sustained disagreement rather than any long
comment thread.

**Trade-offs**

Narrowing the check this way fixed issue-01, issue-04, and (in run 4's variance) issue-19
— all "clear-accept" issues where a bounded task happens to be described as more than one
part. It costs the check's sensitivity to a *quiet* kind of scope failure: `issue-15`
(see Issue analysis) has real, unresolved design uncertainty and two abandoned PRs behind
it, but because the debate reads as a mild clarifying exchange rather than a loud,
sustained argument, and the linked PRs are closed rather than open, neither "Bounded
scope" nor "Unclaimed" catches it. I re-ran `--only issue-15` as part of run 5 (the
7-issue cheap check) and again in run 6 (the full confirming run); it stayed `accept`
both times, so this is the check's actual behavior, not one-off model noise. I accept
this trade-off: the check now correctly handles the common "clear-accept" shape (a
bounded task described in several parts), while `issue-15`'s rare, years-old,
two-abandoned-PR pattern is one of the assignment's stated genuinely arguable scope
calls, and my rubric still clears the category floor on `scope` (3/4) and the overall
bar (19/20).

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to interests and time available:** I'm comfortable across the stack and didn't
   want to over-index on one layer for a first issue, so I weighted this on risk and
   time rather than language. Issue #73 is a two-file text/config mismatch that the
   maintainer estimated at 1-2 hours — the smallest and lowest-risk of the three
   candidates I graded, which fits wanting a small, well-scoped first issue rather than
   an open-ended one.

2. **What the verdict identified correctly, and what I weighed beyond it:** The rubric
   correctly confirmed the mechanical facts — unclaimed, opened by the course
   maintainer, labeled good-first-issue, bounded to two named files, and not blocked by
   any AI-contribution policy (the repo states none). What I weighed that the rubric
   can't: this repo's `docs/CONTRIBUTING.md` requires all five CI jobs green and follows
   strict branch-naming and conventional-commit rules, and several issues carry seeded
   `xfail` tests that have to be un-marked as part of the fix. Issue #73 doesn't touch
   any test fixtures or xfail markers at all — it's the cleanest way to learn the repo's
   process (branch naming, commit format, CI) before I take on an issue where I also
   have to reason about a seeded bug's test suite.

3. **Anticipated difficulty in claiming it:** Low. It's unclaimed, freshly opened
   (2026-09-16), and the Path Review house rule means other students' claim comments
   don't block me even if one shows up first. The main risk is a classmate opening a PR
   for it before I do, since it's an obviously attractive first issue (small, clearly
   scoped, docs-only) — if that happens I'd fall back to #61 or #57, both of which my
   rubric also accepted.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
