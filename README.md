# mirror-demo

Demo of a private source-of-truth repo with a public mirror.

- `mirror-demo-private` (private) is the source of truth.
- `mirror-demo-public` (public) is a SHA-identical mirror of `main`.

## Flow

1. A contributor opens a PR on **mirror-demo-public**; a maintainer reviews it there.
2. A maintainer runs **Import community PR** in mirror-demo-private (Actions → Run workflow → PR number).
   It fetches `pull/<n>/head` from public, pushes it as `community/pr-<n>` and opens a private PR.
3. Internal CI and review run privately. Feedback is relayed to the public PR by hand.
4. Merge the private PR with **Create a merge commit** (not squash, not rebase: they change the SHAs).
5. **Sync to public** pushes `main` to the public repo, and the public PR flips to **Merged** by itself.

Squash or rebase instead, and the public PR stays open; close it with a "Landed in <sha>" comment.
