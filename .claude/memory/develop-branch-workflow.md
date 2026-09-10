---
name: develop-branch-workflow
description: maintainer decision 2026-09-08; both range guards now run on push too (#158), so pre-push duplicates CI rather than substituting for it
metadata:
  type: feedback
---

Maintainer decision, 2026-09-08: **work on `develop`, merge to `main` when green, no pull
requests, and do not wait for confirmation to commit or merge.** This replaces the branch-plus-PR
flow CLAUDE.md described until then.

**Why:** the PR was pure ceremony for a single-maintainer repo. Every gate that mattered already
ran locally, and the review round happened in conversation rather than on the PR.

**How to apply:** commit to `develop`, `git push origin develop`, then `git checkout main && git
merge --ff-only develop && git push origin main`. Watch the `Validate` run on main with `gh run
watch` rather than assuming it passed: there is no PR check standing between a bad commit and
main, so CI is a report after the fact rather than a gate.

**Two consequences, and the first one was missed when this was written.** `validate.yml`
triggered on `pull_request` and `push: [main]` only, so with no PRs there was **no CI on develop
at all** and every check ran for the first time after the merge to main. Fixed by adding `develop`
to the push branches; a code review found it, not the workflow change itself.

The second is now FIXED (#158, 2026-09-08). Both range guards were wired `pull_request`-only, so
they ran in CI on no path; they now run on `push` too, with the base resolved by
`scripts/resolve-range-base.sh` rather than by a YAML expression, because `github.event.before` is
all-zeroes on a created ref and may be unreachable after a force push. **`.githooks/pre-push` now
DUPLICATES CI rather than substituting for it**: its value is giving the same answer before the
push rather than after, so `git config core.hooksPath .githooks` is worth having and `--no-verify`
is a decision rather than a shortcut. The tail of this note used to say the hook was the only
enforcement and that #158 was still open; both were true when written and neither is now.

**Observed across a long session on 2026-09-10, 21 pushes:** the pre-commit hook refused two of
them, each time correctly, and each time for a plugin group changed without a semver bump. On the
largest deletion this repo has made (11 components, one whole group) it was the thing that caught
the omission. Treat a refusal as the guard working, not as friction.

Related: [[bounded-review-loop-in-practice]], [[generated-index-and-size-budget]].
