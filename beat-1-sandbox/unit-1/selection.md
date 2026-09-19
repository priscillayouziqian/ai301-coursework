# Unit 1 — issue selection

## Choose your issue

**Chosen issue:** https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69
— *Output parser crashes on a top-level JSON array fallback*

**Skill verdict: `accept`** (ranked 1st of 3 accepted candidates)

Live-mode run, from `~`:

```
claude "issue-select: grade these candidate first issues: \
  https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68 \
  https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69 \
  https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72"
```

All three were accepted, so the fit profile in `scope.md` did the
ordering: **#69 > #68 > #72**. #69 ranked first because its body says
*what* is broken but not *where* the fallback path lives, so it forces
the codebase navigation I said I wanted. #72 ranked last because it is
the cleanest to finish and therefore teaches the least reading. #68 sits
second only because a classmate claimed it hours earlier — under the
Path Review house rule that does not block it, but between two otherwise
equal issues I would rather take the uncontested one.

The skill's JSON block for the chosen issue:

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
  "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; newest main commit 2026-09-16, 3 days before today (2026-09-19)"},
    {"name": "repo-shipping", "grade": "pass", "evidence": "latest release 'none published' -> fallback: last push to any branch 2026-09-16, 3 days ago (< 90)"},
    {"name": "scope-bounded", "grade": "pass", "evidence": "Names one behavior and its files: 'output_parser.py calls .items() on the parsed value' - rag/generator/output_parser.py, tests/unit/test_output_parser.py; opened by a COLLABORATOR, labeled 'good first issue'"},
    {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; repo has 0 PRs total so no linked PR; comments count 0 - no claim comment exists"},
    {"name": "ai-policy-ok", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI mention; no AI policy file - silence passes"},
    {"name": "maintainer-responsive", "grade": "pass", "evidence": "Issues #52 and #43 each drew a COLLABORATOR reply from Aburke225 on 2026-09-16, ~6 days after opening"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "Labeled 'good first issue' and body lists relevant files under a 'Relevant files' heading"}
  ],
  "verdict": "accept"
}
```

Not claimed yet — per the Unit 1 instructions, choosing is not claiming.
The claim comment comes in Unit 2.
---

## Reflection

**Why this issue, in one sentence?** It is a real Python bug in a repo
that is being actively pushed to, nobody else is on it, and the fix
lives somewhere I will have to go find — which is the skill I most
wanted out of a first contribution.

**What would make you drop it?** Any of my five required checks
flipping: someone opening a PR against it, a maintainer reframing it as
a core-internals change, or the repo adding a contribution policy that
bans AI-assisted work. The fit ranking would not save it — fit only
orders the issues the rubric has already accepted.

**What did writing the rubric teach you that reading the lecture did
not?** That most of the work is not choosing criteria — the four
families were handed to us — but choosing *thresholds*, and that a
threshold is only worth anything if someone else applying it to the same
evidence lands on the same answer. See the Check rationale below.

---

## Run history

Four runs, in order:

1. **Smoke run, `--limit 3`** (issue-01, 02, 03). Scored **2/3**. The two
   rejects landed; `issue-01` came back `reject` against a gold label of
   `accept`, and the note column named `scope-bounded` as the required
   check that sank it (`maintainer-responsive` was also listed, tagged
   `(preferred)`, so it could not have caused the verdict).

2. **Revision, no run.** I opened `issue-01` (conda/conda#16475) and
   `issue-10` (tldr-pages/tldr#18405) side by side. Both bodies are a
   list of headed items, and my first `scope-bounded` wording asked
   whether the body was "a list of sub-items meant to be split into
   separate pull requests" — a question about the author's intent that
   the two issues answer identically on the page. I rewrote the check to
   lead with a positive, checkable test (does the body name a target?)
   instead of a negative one about list-shape.

3. **Targeted re-run, `--only issue-01,issue-05,issue-14,issue-19,issue-20`**
   (~$1 instead of ~$4). I picked the five issues that stress the
   rewritten check from both sides: the two long named-file lists that
   must pass (01, 14), the list-of-causes bug that must pass (19), and
   the two that must still fail (05, codebase-wide type annotations; 20,
   a feature wish with an open product decision). Scored **5/5**.

4. **Full run, `--save-run eval-run.txt`.** Scored **20/20**, with every
   category matched: `claimed 4/4, clear-accept 8/8, dead-repo 3/3,
   policy 1/1, scope 4/4`. This is the run in `eval-run.txt`.

I did not touch `rubric.md` after run 4: the header the harness wrote
records `rubric.md sha256:ff586ce2bd151eb7`, and the rubric in the skill
I uploaded still hashes to `ff586ce2...`, so the file being graded and
the file being read are the same file.
---

## Issue analysis

**`issue-01` — conda/conda#16475, "Add permanent docs for installing
PyPI packages with `conda install`".** My rubric: **accept**. Gold label:
**accept**. Agreed — but this is the issue my rubric got *wrong* on the
first run, and why it was wrong is the most useful thing I learned.

The bundle is a documentation request whose body is a `## Proposed
changes` section broken into four sub-headings: add a new task page,
update `manage-pkgs.rst`, update `pip-interoperability.rst`, update
`new-features.md`, plus a fifth "consider a global `troubleshooting.rst`
entry" marked lower priority. Every other family is uncontroversial —
conda pushed to `main` the day before capture, released 26.7.0 five days
before it, the issue has `assignees: none` and `linked PRs: none`, and
CONTRIBUTING explicitly welcomes generative AI. So the verdict rested
entirely on `scope-bounded`.

My first wording failed it, and the failure was reasonable on its own
terms: five headed work items really does look like something you would
split across PRs. What the gold note says is *"docs task with a stated
home and scope"* — the grader read the same five headings as one
deliverable, because each one names a specific file in this repository
and says what to change in it.

The comparison that settled it for me is `issue-10` (tldr-pages/tldr
#18405, gold `reject`), whose body is also a list:

```
issue-01  ->  ### Update manage-pkgs.rst        (a file in this repo)
issue-10  ->  - #5070                           (another issue to go do)
```

Visually the same shape; structurally opposite. One list is the *spec
for one change*; the other is a *queue of other people's work*. My
original check could not tell them apart because it asked what the list
*meant*. The rewritten check asks what the list *points at*, which is a
fact you can read off the page — and on the full run it separated all
four scope issues correctly (01, 14, 19 accept; 05, 10, 15, 20 reject).

---

## Check rationale

The check I rewrote is `scope-bounded`. Its pass condition now opens:

> First apply the **bounded test**: the issue is bounded when it names a
> target — one specific behavior to change or fix, or a specific set of
> files, pages, or modules and what to change in each. A bounded issue
> passes, **however many targets it names and however long the list
> is**; assume one pull request delivers all of them unless the issue
> says otherwise.

Three deliberate choices in that sentence:

**It is positive, and it runs first.** The five disqualifiers that follow
it (umbrella/tracking, codebase-wide with no endpoint, unsettled design
debate, support question, open product decision) only get consulted if
the bounded test does not already settle the issue. Leading with the
negative list is what made my first version fail `issue-01`: a
disqualifier fired before anything had established that the issue was
fine.

**"Names a target" is a fact, not a judgement.** The rubric template
asks for conditions "someone else could apply and get your answer", and
recommends numeric thresholds. Three of my checks can be numeric —
`repo-alive` is 180 days, `repo-shipping` is 365, `unclaimed` is 180 —
but scope has no number in it. The substitute for a number is a question
with an observable answer. *Does the body name files or a behavior in
this repository?* is answerable by pointing at the text. *Is this too
big for a newcomer?* is not.

**"However many targets it names and however long the list is" is doing
real work.** Without that clause the check silently reintroduces a
length heuristic, and length is exactly the wrong signal here:
`issue-04` (gold `accept`) is one sentence long, `issue-01` and
`issue-14` (both gold `accept`) are among the longest bodies in the set,
and `issue-20` (gold `reject`) is a tidy, well-formatted template with
no target at all. The check also names what does *not* fail it — a terse
body, a missing reproduction, a years-old issue, a list of named causes
inside one bug — so that the grader does not fall back on polish as a
proxy for scope.

---

## Trade-offs

**Maintainer responsiveness is `preferred`, not `required` — and that is
a real hole.** A repo can be pushing commits daily and still never answer
an issue, which leaves your PR unreviewed forever; that is precisely the
failure Family 1 exists to catch, and my rubric cannot reject on it. I
accepted the hole because the alternative is worse: `issue-14`'s
response sample is a single line reading `no maintainer comment in
thread`, and `issue-06` shows four such lines out of five, yet both are
gold `accept`. Any required threshold on that field rejects them and
takes down the `clear-accept` category. The signal is too sparse in small
and young repos to gate a verdict on, so it ranks instead of deciding.

**The 180-day claim window is the weakest number in the rubric.** It is
calibrated to a gap, not to a principle: `issue-09`'s stale claim is
1,658 days old and `issue-18`'s live one is 3 days old, so anything in
between separates them. A real contributor who claims an issue and goes
quiet for four months would be read as still active; one who goes quiet
for seven would be read as gone. Neither reading is obviously right, and
I have no evidence in this set that distinguishes them.

**`unclaimed` treats a `merged` linked PR as a claim.** That is right
when the merge fixed the issue and it simply has not been closed, and
wrong when a large issue has landed one of several planned PRs and still
wants help. No accepted issue in this eval set has a merged linked PR, so
the set could not have taught me the difference — this is a threshold
that passed eval without ever being tested.

**`ai-policy-ok` fails only on an outright ban, which I think is
slightly too permissive.** `issue-10`'s policy says PRs *"suspected of
being made wholly or partly with generative AI ... are closed"* — in
practice that is a ban with softer wording, but it passes my check
because it is phrased as discouragement plus a condition. It cost
nothing here (`issue-10` rejects on scope anyway), but on a live issue it
would send me into a repo that will close my PR on suspicion. The
evidence guide's "conditions are not bans" rule is the right default; the
line between a strict condition and a ban in disguise is one my current
wording cannot draw.

**Binary verdict, no scoring.** Any single required fail rejects,
regardless of how strong the other four are. This throws away real
information — `issue-12` is an excellent issue in a healthy repo that
loses only on contribution policy — but the alternative, weighting the
checks and summing, would let three strong signals outvote a
disqualifying one. Each required check names an independent way the
contribution dies, and you cannot compensate for a dead repo with a
well-written issue body.