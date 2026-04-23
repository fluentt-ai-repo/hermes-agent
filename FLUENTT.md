# Fluentt fork

Downstream fork of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) maintained by [@5Hyeons](https://github.com/5Hyeons) for the [daymo-unity](https://github.com/fluentt-ai-repo/daymo-unity) project.

This fork exists as a **thin patch layer** — packaging and compatibility fixes that haven't landed upstream yet. Substantive behavior changes go upstream whenever possible. Anyone not building daymo should use [upstream](https://github.com/NousResearch/hermes-agent) instead.

## Branches

| Branch | Role |
|--------|------|
| `main` | Upstream mirror. Synced from `NousResearch/hermes-agent` daily by CI (see `.github/workflows/fluentt-upstream-sync.yml`). Never edit directly. |
| `fluentt/main` | daymo's pin target. `main` + our patches. |

daymo pins to a specific `fluentt/main` SHA in its `agent-backend/pyproject.toml`.

## Patch policy

- Each fluentt commit's subject starts with `[fluentt]` for grep-ability: `git log --grep='^\[fluentt\]'`.
- One logical change per commit.
- Prefer upstream PR first; only land in fork when upstream merge is uncertain or slow.
- Track every patch in [`DIVERGENCE.md`](./DIVERGENCE.md). When upstream absorbs one of our patches, move that row to the "historical" section and drop the commit on next rebase.

## Bumping — syncing with upstream

CI runs a fast-forward of `main` from `upstream/main` daily. If it can't fast-forward (unexpected — `main` should never diverge locally), the workflow leaves `main` alone and exits so a human can investigate.

Once `main` is refreshed, rebase `fluentt/main`:

```bash
git fetch origin
git checkout fluentt/main
git rebase origin/main
# resolve conflicts — typically only pyproject.toml in the packaging patch
git push --force-with-lease origin fluentt/main
```

After rebase:

1. Run wheel smoke test: `python -m build --wheel && python -m zipfile -l dist/*.whl | grep agent/transports/__init__.py` — if present, the packaging patch is still needed.
2. If upstream absorbed the fix, drop our commit (`git rebase -i` → drop) and update `DIVERGENCE.md`.
3. Grab the new `fluentt/main` SHA, update daymo's `agent-backend/pyproject.toml`, run daymo bootstrap + `/chat` smoke locally before merging daymo PR.

## Maintainer

[@5Hyeons](https://github.com/5Hyeons) — email in GitHub profile. Ping for merges, conflict resolution, or upgrade decisions.
