# Divergence from upstream

List of patches on `fluentt/main` relative to the branch base. See [`FLUENTT.md`](./FLUENTT.md) for the bump workflow that prunes this list over time.

## Active

Patches currently applied on top of `main`.

| Commit | Subject | Upstream status | Notes |
|--------|---------|-----------------|-------|
| [`4d6019d2`](https://github.com/fluentt-ai-repo/hermes-agent/commit/4d6019d2a37d820c71402505e7cbd753aad7907f) | `[fluentt] fix(packaging): include agent.* subpackages in wheel` | Fixed upstream post-`ff9752410`. | Will drop to a no-op on next rebase past the upstream fix commit — delete from this table and move to "Historical". |

## Historical

Patches that upstream has absorbed and we have dropped from `fluentt/main`.

*(none yet)*

## How to add a row

1. Land the commit on `fluentt/main` with `[fluentt]` prefix.
2. Add a row above with the short SHA, subject, and current upstream status (`open PR #...`, `not submitted`, `fixed upstream post-<SHA>`, etc).
3. On next upstream rebase, reassess each row. Move absorbed patches to Historical and drop the corresponding commit.
