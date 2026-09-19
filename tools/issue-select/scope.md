# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s3` <!-- paste your section's repo from the Unit 1 Check-In page -->

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

<!-- YOU write this part: a few sentences about you. What languages and
tools you have actually used, what you want to get better at, anything
you want to avoid. The skill uses this only to RANK the issues your
rubric accepts, never to change a verdict: fit cannot rescue an issue
your rubric rejects, and cannot sink one it accepts. -->

I have actually shipped code in JavaScript and TypeScript, in React and
React Native on the front end, and in Node/Express with Firebase on the
back end. I am comfortable in Python for scripts, data wrangling, and
small backends. My own projects have been ones I set up myself, so the
thing I most want out of a first contribution is the part I have never
done: going end to end through somebody else's open-source process —
fork, branch, a PR that follows their conventions, and surviving a real
code review. Right behind that, I want practice reading a large codebase
I did not write and finding my way to the few lines that matter.

So, among the issues my rubric accepts, rank higher: issues in
JS/TS/React or Python; issues whose body names the files or directory to
start in, since that is a short on-ramp into an unfamiliar tree; and
issues in repos whose CONTRIBUTING spells out the PR process, since
following a real process is the point. Rank lower: issues that are pure
copy edits with no code reading in them, and issues whose main work is
in a language I have not written (Go, Rust, C++) or in build, packaging,
or CI infrastructure, where I cannot yet tell a correct fix from one
that merely passes.
