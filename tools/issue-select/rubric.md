# Rubric: is this a good first issue?

Five required checks, one per failure mode that actually kills a first
contribution, plus two preferred checks that only rank the issues the
required five accept.

Every date threshold below is measured against the **capture date stamped
at the top of the bundle** (eval mode) or against **today** (live mode) —
never against the date you happen to be reading this.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `repo-alive` | Repo facts: the `archived:` flag on the repo line, and the dates on the "last 5 default-branch commits" list. | `archived:` is `no` AND the newest of the last 5 default-branch commits is dated within **180 days** of the capture date. An archived repo is read-only and fails outright, whatever its commit history says. Bot-authored commits count as life when the commit is merging a human's pull request. | required |
| `repo-shipping` | Repo facts: the "latest release" line and the "last push to any branch" line. | The latest release is dated within **365 days** of the capture date. If the line reads `none published`, this check instead passes when "last push to any branch" is within **90 days** of the capture date — plenty of healthy projects ship from the default branch and never cut a GitHub release, so absence of releases is only damning when the branch is also quiet. | required |
| `scope-bounded` | The issue title, body, labels, and the opener's association, plus the whole comment thread. | First apply the **bounded test**: the issue is bounded when it names a target — one specific behavior to change or fix, or a specific set of files, pages, or modules and what to change in each. A bounded issue passes, **however many targets it names and however long the list is**; assume one pull request delivers all of them unless the issue says otherwise. Only if it is NOT bounded, or if one of the following is true, does the check fail: <br> (a) the body's substance is a list of *other issue numbers* to go work on, or the issue calls itself a tracking, mega, or umbrella issue; <br> (b) the target is the codebase as a whole with no named endpoint ("add X everywhere", "incrementally add more Y", "PRs welcome big and small") rather than a named behavior or a named set of files; <br> (c) the thread is still arguing the design and no OWNER, MEMBER, or COLLABORATOR has settled it, or a maintainer says the fix needs changes to core internals; <br> (d) the issue is a usage or support question ("how do I get this to work?") rather than a request for a change; <br> (e) it is a feature request that still leaves a product or design decision open AND no OWNER/MEMBER/COLLABORATOR filed it, endorsed it in the thread, or put a `good first issue` label on it. <br> None of these fail the check on their own: a terse one-line body, a missing reproduction, an issue open for years, a list of named causes or acceptance criteria inside one bug, section headings that enumerate the named files to edit, or a change spanning several named files. Grade the size of the work asked for, not the polish or the length of the writeup. | required |
| `unclaimed` | Repo facts: the `this issue: assignees:` and `linked PRs:` fields, plus every comment in the Comments section with its date. | Passes only when **all** of: `assignees:` is `none`; no linked PR is in state `open` or `merged`; and no comment claiming the work ("I'll take this", "can I work on this", "working on this", "I'd like to take this") is dated within **180 days** of the capture date. A linked PR in state `closed` is an abandoned attempt, not a claim, and a claim comment older than 180 days is stale — both pass, and both are worth a line in the summary. A bot nudging an assignee about inactivity does not release the claim; only an explicit hand-back does. | required |
| `ai-policy-ok` | Repo facts: the "contribution policy" line, including whatever `CONTRIBUTING.md`, a linked contributor site, or a dedicated AI-policy file is quoted there. | Fails only on an **outright ban** on AI-assisted or AI-generated contributions ("we do not accept AI-generated code or documentation"). Everything short of a ban passes: silence, no `CONTRIBUTING.md` at all, an explicit welcome, discouragement without prohibition, and conditions of any strictness (disclose AI use, personally understand and test every change, human-review AI output, PRs that look untested get closed). Conditions are terms to follow, not reasons to walk away; this course's workflow is AI-assisted, so a stated ban is a dead end before a maintainer reads a line of the code. | required |
| `maintainer-responsive` | Repo facts: the "maintainer first-response sample" list of recently updated issues and days to first owner/member/collaborator comment. | At least 2 sampled issues received a first maintainer reply at all, and at least one of those replies came within 30 days. Never changes a verdict — a small or quiet project can be perfectly alive with a thin sample, which is why this is preferred and `repo-alive` is required. Use it to prefer the accepted issue whose maintainers answer fastest. | preferred |
| `newcomer-signposted` | The issue's labels, and the body's closing sections. | The issue carries a `good first issue`, `help wanted`, or `easy` label, OR the body names where to start (files, directories, modules) or spells out acceptance criteria or a contribution walkthrough. Never changes a verdict: an unlabeled, unsignposted issue can still be a fine first contribution. Use it to rank accepted issues by how little guessing the first pull request will need. | preferred |

## Verdict rule

**Accept** if and only if all five `required` checks grade `pass`. Any
single required `fail` produces **reject** — there is no scoring, no
averaging, and no number of passes that outweighs one fail, because each
required check names an independent way the contribution dies.

`unclear` counts as `fail` on a required check: a first issue whose
liveness, scope, claim status, or contribution policy you cannot verify
from the evidence is not a first issue worth taking. On a preferred check
`unclear` is simply reported and changes nothing.

`preferred` checks never enter the verdict. Report their grades, and on an
accepted issue cite them in the summary as the reason to prefer it over
other accepted candidates.
