---
name: sync-opencode-fork
description:
  Keeps the danfrenette/opencode `dan-dev` fork rebased onto upstream OpenCode V2, then production
  after V2 ships. Use when updating the fork, rebasing `dan-dev`, checking whether V2 reached a
  GitHub release, or coordinating upstream conflicts with the resolving-merge-conflicts skill.
---

# Sync OpenCode Fork

Keep `fork/dan-dev` as the fork's patch stack over the correct upstream channel. Establish the
fork's intent from its current patch stack, checkout instructions, and linked PR or issue sources
before rebasing.

## Preconditions

1. Locate the OpenCode checkout and read its `AGENTS.md` files.
2. Confirm `origin` is `anomalyco/opencode` and `fork` is `danfrenette/opencode`.
3. Require `gh auth status` to succeed and the worktree to be clean, with no rebase, merge, or
   cherry-pick in progress.
4. Fetch both remotes with pruning. Never discard local work to make the preconditions pass.
5. Require local `dan-dev` and `fork/dan-dev` to exist and resolve to the same commit. If they
   diverge, stop and report both SHAs.

Preconditions are complete only when the fetched refs are current and the exact starting SHA of
`fork/dan-dev` is recorded for the lease and final report.

## Choose The Base

The production branch is upstream `dev`, not `main` or `production`.

Use `branch.dan-dev.opencode-base` as a local persistent marker with value `v2` or `dev`. Default to
`v2` when it is unset. Hold a detected channel change in memory until verification succeeds; a
failed rebase must not change the marker.

Switch the marker to `dev` when either condition is true:

- The user explicitly says V2 is released or directs the fork onto production.
- The latest published, non-draft, non-prerelease GitHub release tag contains the last synchronized
  V2 commit.

Use
`gh release view --repo anomalyco/opencode --json tagName,publishedAt,url,isDraft,isPrerelease,targetCommitish`,
fetch its tag, and prove containment with `git merge-base --is-ancestor`. Read the last V2 commit
from `branch.dan-dev.last-v2`; when unset, use `git merge-base fork/dan-dev origin/v2`. A release is
evidence only when its tag commit contains that exact commit. Report the release URL when switching.

Select `origin/v2` for marker `v2` and `origin/dev` for marker `dev`. If required refs or release
evidence cannot be established, stop rather than infer a base from branch names or dates.

Base selection is complete only when the selected remote ref, its SHA, the marker value, and any
release evidence are recorded.

## Rebase

1. Switch to `dan-dev` and record its old merge-base with the selected upstream ref.
2. If the selected upstream tip is already an ancestor of `dan-dev`, skip rewriting history and
   continue to verification.
3. Rebase `dan-dev` onto the selected upstream ref.
4. If conflicts occur, immediately invoke the installed `/resolving-merge-conflicts` skill. Do not
   resolve hunks through this skill.
5. Give the conflict skill the merge goal: retain the behavior established from the fork patches and
   their sources on current upstream architecture without inventing new behavior. Provide the old
   fork SHA, old merge-base, selected base SHA, conflicted paths, fork commit messages, and relevant
   PR or Linear sources.
6. Let `/resolving-merge-conflicts` inspect primary sources, resolve every hunk, run its discovered
   checks, and continue until the entire rebase finishes. Resume this workflow at verification only
   after it returns.

The rebase is complete only when Git reports no operation in progress, the worktree is clean, the
selected base is an ancestor of `dan-dev`, and
`git range-diff <old-merge-base>..<old-fork-sha> <base>..dan-dev` accounts for every old fork patch
as a rebased patch or an upstream equivalent.

## Verify

Inspect the upstream delta, rebased fork delta, and any conflict resolutions. Follow every
applicable repository/package `AGENTS.md` instruction.

- Run `git diff --check <base>...dan-dev`.
- Inspect the complete `git range-diff` for dropped or materially changed fork behavior.
- Run typechecks and focused tests for packages affected by the upstream delta or fork patch stack.
- Run generated-client checks when public Protocol or Server `HttpApi` changed.
- Run session/timeline production benchmarks when those surfaces changed.
- Run tests from package directories, never the repository root.

Verification is complete only when every applicable check passes. Treat unrelated known failures as
blockers unless their pre-existing status is demonstrated from current evidence.

## Publish

Push only after verification:

```bash
git push --force-with-lease=refs/heads/dan-dev:<recorded-old-fork-sha> fork dan-dev:dan-dev
```

After successful verification and any required push, persist the selected channel in
`branch.dan-dev.opencode-base`. For a V2 run, set `branch.dan-dev.last-v2` to the synchronized
`origin/v2` SHA. Confirm local `dan-dev` and `fork/dan-dev` match.

Report the old and new fork SHAs, selected base and SHA, production-release evidence, conflicts
resolved, checks run, and push result. A no-op run reports the same base evidence and performs no
push.
